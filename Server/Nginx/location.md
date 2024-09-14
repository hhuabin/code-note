# location

**匹配规则的优先级顺序**

1. **精确匹配 (`=`)**
2. **前缀匹配，使用通配符 (`^~`)**
3. **正则匹配 (`~` 和 `~\*`)**
4. **前缀匹配（默认）**

匹配规则

1. 精确匹配

   ```nginx
   location = /exact {
       # 当请求的 URI 完全是 "/exact" 时匹配此规则
       ...
   }
   ```

2. 前缀匹配，使用通配符 (`^~`)

   ```nginx
   location ^~ /static/ {
       # 匹配所有以 "/static/" 开头的 URI，并停止正则匹配
       ...
   }
   ```

3. 正则匹配 (`~` 和 `~\*`)

   ```nginx
   location ~ \.php$ {
       # 匹配以 ".php" 结尾的 URI，区分大小写
       ...
   }
   
   location ~* \.jpg$ {
       # 匹配以 ".jpg" 结尾的 URI，不区分大小写
       ...
   }
   ```

4. 前缀匹配（默认）

   ```nginx
   location /images/ {
       # 匹配所有以 "/images/" 开头的 URI
       ...
   }
   ```



## proxy_pass（负载均衡）

1. proxy_pass

   `proxy_pass`与`root`、`index`是冲突的，配置了`proxy_pass`就不用配置`root`、`index`

   对服务器的请求会被代理到proxy_pass后面的网址去，后面的网址默认使用 `http` 协议(不配置就使用http)，不能使用https(证书关系)

   单个反向代理

   ```nginx
   server {
   	location / {
           proxy_pass bilibili.com;
           # proxy_pass 192.168.0.1:80;
           # root   /bin2;
           # index  index.html index.htm;
       }
   }
   ```

2. 反向代理一组服务(平均负载)

   ```nginx
   upstream yourname {
   	server 192.168.0.1:80;
   	server 192.168.0.2:80;
   }
   
   server {
   	location / {
           proxy_pass yourname;
           # root   /bin2;
           # index  index.html index.htm;
       }
   }
   ```

3. 权重负载均衡(weight)

   按照配置weight的比例来分权

   ```nginx
   upstream httpds {
   	server 192.168.0.1:80 weight 8;
   	server 192.168.0.2:80 weight 2;
   }
   ```

4. `down`、`backup`

   `down`：ip已下线，不会代理到此服务器中

   `backup`：备用服务器，正常情况下不会代理到此服务器中，当其他服务器不能使用时，使用该服务器

   ```nginx
   upstream httpds {
   	server 192.168.0.1:80 weight 8 down;
   	server 192.168.0.2:80 weight 2 backup;
   }
   ```

5. `ip_hash`、`least_conn`、`url_hash`、`fair`

   以上基本不用，都有各式的问题，可以用其他方式解决

   `ip_hash`：通过计算客户端 IP 地址的哈希值，将每个客户端的请求固定分配到特定的后端服务器。虽然 `ip_hash` 有助于**保持会话的一致性**（即同一客户端的请求始终分配到同一台后端服务器），但也可能会带来一些不利影响，如负载不均衡、不支持`backup`等。不使用`ip_hash`可以使用cookie、token等方式解决



## 动静分离

/css、/js、/img下的请求会在本机服务器获取。其他请求会被代理到192.168.0.1:80

```nginx
server {
	location / {
        proxy_pass 192.168.0.1:80;
        # root   /bin2;
        # index  index.html index.htm;
    }
    
    location /css {
        root   html;
        index  index.html index.htm;
    }
    
    location /js {
        root   html;
        index  index.html index.htm;
    }
    
    location /img {
        root   html;
        index  index.html index.htm;
    }
    
    # 也可以是使用正则
    # location ~*/(css|js|img) {
    #     root   html;
    #     index  index.html index.htm;
    # }
}
```



## rewrite

`rewrite` 是 Nginx 中用于重写或修改请求 URI 的指令。通过 `rewrite` 指令，可以根据一定的规则将请求重定向到另一个 URI 或者内部处理不同的请求路径，也可用于隐藏真正的请求路径

rewrite指令语法

```nginx
location {
	rewrite regex replacement [flag];
}
```

- **`regex`**：正则表达式，用于匹配请求的 URI
- **`replacement`**：匹配成功时，将请求 URI 重写为这个值
- **`flag`**：可选参数，用于指定重写的行为
  - **`last`**：**默认值**。停止重写并将请求转发到新的位置，继续向下匹配。(可隐藏真实请求地址)
  - **`break`**：停止重写，并且不再向下匹配。(可隐藏真实请求地址)
  - **`redirect`**：返回 HTTP 302 临时重定向。
  - **`permanent`**：返回 HTTP 301 永久重定向

---

1. 简单的重写规则

   ```nginx
   location /old-path {
       rewrite ^/old-path(.*)$ /new-path$1 permanent;
   }
   ```

   匹配所有以 `/old-path` 开头的请求，并将其重定向到 `/new-path`，使用 HTTP 301 永久重定向。

   例如：`/old-path/test` 将被重定向到 `/new-path/test`

2. 去掉 URI 中的特定部分

   ```nginx
   location / {
       rewrite /images/(.*)$ /pics/$1 last;
   }
   ```

   将 URI 中的 `/images/` 部分替换为 `/pics/`，并停止重写

   例如：`/images/photo.jpg` 会被内部重写为 `/pics/photo.jpg`

3. 根据条件重写

   ```nginx
   location / {
       if ($http_user_agent ~* MSIE) {
           rewrite ^(.*)$ /msie.html break;
       }
   }
   ```

   如果用户代理（浏览器）是 Internet Explorer，则将请求重写为 `/msie.html`，并停止重写。

   `$http_user_agent` 是一个内置变量，表示请求的用户代理字符串

4. 使用正则表达式进行重写

   ```nginx
   location / {
       rewrite ^/product/([0-9]+)/?$ /show_product.php?id=$1 break;
   }
   ```

   将 `/product/123` 的请求重写为 `/show_product.php?id=123`，并停止重写

   `([0-9]+)` 匹配一个或多个数字，并将其作为参数传递给 `replacement`

5. 配合 `try_files` 实现更复杂的重写逻辑

   ```nginx
   location / {
       try_files $uri $uri/ /index.php?$args;
   }
   ```

   尝试访问请求的 URI，如果失败，则尝试访问目录形式的 URI（在结尾加上 `/`），最后如果仍然无法匹配，则重写为 `/index.php` 并传递原始的查询参数 `$args`

**`rewrite` 指令的注意事项**

1. **性能考虑**：过多的 `rewrite` 规则可能影响 Nginx 的性能，因为每个请求都需要进行正则匹配。
2. **优先级和顺序**：`rewrite` 规则按顺序匹配，因此顺序非常重要，放在前面的规则优先级更高。
3. **避免无限重写**：使用 `rewrite` 时要防止出现无限重写循环，例如同一个 URI 不断被重写为相同的 URI



