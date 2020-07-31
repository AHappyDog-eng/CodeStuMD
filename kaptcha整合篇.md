# springboot 整合kaptcha 实现验证码



### 1. 导入 kaptcha maven依赖

```xml
        <dependency>
            <groupId>com.github.penggle</groupId>
            <artifactId>kaptcha</artifactId>
            <version>2.3.2</version>
        </dependency>

```

### 2. kaptcha的常用配置

`

| **选项**                         | **描述**                                                     | **默认值**                                            |
| -------------------------------- | ------------------------------------------------------------ | ----------------------------------------------------- |
| kaptcha.border                   | 图片边框，合法值：yes , no                                   | yes                                                   |
| kaptcha.border.color             | 边框颜色，合法值： r,g,b (and optional alpha) 或者 white,black,blue. | black                                                 |
| kaptcha.border.thickness         | 边框厚度，合法值：>0                                         | 1                                                     |
| kaptcha.image.width              | 图片宽                                                       | 200                                                   |
| kaptcha.image.height             | 图片高                                                       | 50                                                    |
| kaptcha.producer.impl            | 图片实现类                                                   | com.google.code.kaptcha.impl.DefaultKaptcha           |
| kaptcha.textproducer.impl        | 文本实现类                                                   | com.google.code.kaptcha.text.impl.DefaultTextCreator  |
| kaptcha.textproducer.char.string | 文本集合，验证码值从此集合中获取                             | abcde2345678gfynmnpwx                                 |
| kaptcha.textproducer.char.length | 验证码长度                                                   | 5                                                     |
| kaptcha.textproducer.font.names  | 字体                                                         | Arial, Courier                                        |
| kaptcha.textproducer.font.size   | 字体大小                                                     | 40px                                                  |
| kaptcha.textproducer.font.color  | 字体颜色，合法值： r,g,b  或者 white,black,blue.             | black                                                 |
| kaptcha.textproducer.char.space  | 文字间隔                                                     | 2                                                     |
| kaptcha.noise.impl               | 干扰实现类                                                   | com.google.code.kaptcha.impl.DefaultNoise             |
| kaptcha.noise.color              | 干扰颜色，合法值： r,g,b 或者 white,black,blue.              | black                                                 |
| kaptcha.obscurificator.impl      | 图片样式：水纹com.google.code.kaptcha.impl.WaterRipple鱼眼com.google.code.kaptcha.impl.FishEyeGimpy阴影com.google.code.kaptcha.impl.ShadowGimpy | com.google.code.kaptcha.impl.WaterRipple              |
| kaptcha.background.impl          | 背景实现类                                                   | com.google.code.kaptcha.impl.DefaultBackground        |
| kaptcha.background.clear.from    | 背景颜色渐变，开始颜色                                       | light grey                                            |
| kaptcha.background.clear.to      | 背景颜色渐变，结束颜色                                       | white                                                 |
| kaptcha.word.impl                | 文字渲染器                                                   | com.google.code.kaptcha.text.impl.DefaultWordRenderer |
| kaptcha.session.key              | session key                                                  | KAPTCHA_SESSION_KEY                                   |
| kaptcha.session.date             | session date                                                 | KAPTCHA_SESSION_DATE                                  |

`

### 3. pom.xml中的常用配置

```.xml
kaptcha:
  border: "yes"					#是否有边框，默认为yes
  border.color: 105,179,90		 #边框颜色
  textproducer:			
    font:
      color: blue				#验证码字体颜色
      size: 30					#文本字符大小
      names: 宋体,楷体,微软雅黑	   #文本字体样式
    char:
      length: 4			#验证码文本字符长度
  image:
    width: 120			# 图片宽度
    height: 40			# 图片高度
  session:
    key: code			# 存储session key

```

### 4. 注册加入IOC容器

```java
package com.examsystem.configuraction.kaptcha;

import com.google.code.kaptcha.impl.DefaultKaptcha;
import com.google.code.kaptcha.util.Config;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import java.util.Properties;

/*
 *@Author WN
 *@date 2020/3/27 13:19
 */
@Configuration
public class kaptchaConfig {

    @Bean
    public DefaultKaptcha getDefaultKapcha(){
        DefaultKaptcha defaultKaptcha = new DefaultKaptcha();
        Properties properties = new Properties();
        properties.setProperty("kaptcha.border", "yes");
        // 边框颜色
        properties.setProperty("kaptcha.border.color", "105,179,90");
        // 字体颜色
        properties.setProperty("kaptcha.textproducer.font.color", "red");
        // 图片宽
        properties.setProperty("kaptcha.image.width", "110");
        // 图片高
        properties.setProperty("kaptcha.image.height", "40");
        // 字体大小
        properties.setProperty("kaptcha.textproducer.font.size", "30");
        // session key
        properties.setProperty("kaptcha.session.key", "code");
        // 验证码长度
        properties.setProperty("kaptcha.textproducer.char.length", "4");
        // 字体
        properties.setProperty("kaptcha.textproducer.font.names", "宋体,楷体,微软雅黑");
        Config config = new Config(properties);
        defaultKaptcha.setConfig(config);

        return defaultKaptcha;
    }

}

```

### 5. 返回一个实例defaultKaptcha之后就可以直接用了

##### 	可以考虑生成工具类，或者直接写到映射Controller中 按照业务来写，我写的是在Controller业务层中

```
package com.examsystem.controller.image;

import com.alibaba.fastjson.JSON;
import com.examsystem.tools.statuscode;
import com.google.code.kaptcha.impl.DefaultKaptcha;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.servlet.ModelAndView;

import javax.imageio.ImageIO;
import javax.naming.spi.DirStateFactory;
import javax.servlet.ServletOutputStream;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.awt.image.BufferedImage;
import java.io.ByteArrayOutputStream;
import java.io.IOException;

/*
 *@Author WN
 *@date 2020/3/27 13:21
 */
@Controller
public class imageConfig {
    @Autowired
    private DefaultKaptcha defaultKaptcha;

    @RequestMapping("/Kaptcha/Generate")
    public void defaultKaptcha(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse)
            throws Exception {
        byte[] captchaChallengeAsJpeg = null;
        ByteArrayOutputStream jpegOutputStream = new ByteArrayOutputStream();
        try {
            // 生产验证码字符串并保存到session中
            String createText = defaultKaptcha.createText();
            httpServletRequest.getSession().setAttribute("rightCode", createText);
            // 使用生产的验证码字符串返回一个BufferedImage对象并转为byte写入到byte数组中
            BufferedImage challenge = defaultKaptcha.createImage(createText);
            ImageIO.write(challenge, "jpg", jpegOutputStream);
        } catch (IllegalArgumentException e) {
            httpServletResponse.sendError(HttpServletResponse.SC_NOT_FOUND);
            return;
        }

        // 定义response输出类型为image/jpeg类型，使用response输出流输出图片的byte数组
        captchaChallengeAsJpeg = jpegOutputStream.toByteArray();
        httpServletResponse.setHeader("Cache-Control", "no-store");
        httpServletResponse.setHeader("Pragma", "no-cache");
        httpServletResponse.setDateHeader("Expires", 0);
        httpServletResponse.setContentType("image/jpeg");
        ServletOutputStream responseOutputStream = httpServletResponse.getOutputStream();
        responseOutputStream.write(captchaChallengeAsJpeg);
        responseOutputStream.flush();
        responseOutputStream.close();
    }

    /**
     * 3、校对验证码
     */
    @RequestMapping("/Kaptcha/judge")
    @ResponseBody
    public String imgvrifyControllerDefaultKaptcha(HttpServletRequest httpServletRequest,
                                                         HttpServletResponse httpServletResponse) {
        ModelAndView andView = new ModelAndView();
        String rightCode = (String) httpServletRequest.getSession().getAttribute("rightCode");
        String tryCode = httpServletRequest.getParameter("tryCode");
        if (!rightCode.equals(tryCode)) {
            return JSON.toJSONString(new statuscode(false,401,"验证码错误"));
        } else {
            return JSON.toJSONString(new statuscode(true,20000,"成功"));
        }
    }

}

```

### 6. 在浏览器中访问，查看是否成功

##### 	成功显示

![1585288204162](C:\Users\lenovo\AppData\Local\Temp\1585288204162.png)



注意： statuscode 是我自己项目中自定义的类，是基于vue来的，前后端不分离可以存ModelAndView中