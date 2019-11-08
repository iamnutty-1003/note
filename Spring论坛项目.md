# Spring论坛项目

地址[https://www.bilibili.com/video/av50200264](https://www.bilibili.com/video/av50200264)

## 运行第一个Springboot项目

GUIDES地址[https://spring.io/guides](https://spring.io/guides)

Spring Initializr[https://start.spring.io/](https://start.spring.io/)

~~~java
@Controller
public class HelloController {

    @GetMapping("/hello") //只处理Get请求
    
    public String hello(@RequestParam(name="name") String name, Model model){
        model.addAttribute("name",name);
        return "hello"; //找模板目录templates/hello.html
    }
}
~~~

然后访问[http://localhost:8080/hello?name=LSN](http://localhost:8080/hello?name=LSN)

## 使用Git管理项目

创建项目-->deploy keys(给了keys才能提交代码)

## 引入jquery bootstrap

[https://v3.bootcss.com](https://v3.bootcss.com/)

引入dependency [https://www.webjars.org](https://www.webjars.org/)

## 注册Github app

实现Github登录功能