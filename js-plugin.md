
## swiper 轮播图
---

- [swiper.js 官网](https://www.swiper.com.cn/)
  - [swiper4.x API](https://www.swiper.com.cn/api/index.html)

> 

```
```

!> 未完待续...

<br>
<br>
<br>

## particles 粒子效果
---

- particles.js 官网
  - https://link.juejin.im/?target=http%3A%2F%2Fvue-particles.netlify.com%2F


- 安装方式
  - `npm install particles.js`

- 使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>canvas-粒子特效</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body, html {
      margin: 0;
      padding: 0;
      width: 100%;
      height: 100%;
    }
    #particles-js {
      width: 100%;
      height: 100%;
      background-color: #333;
    }
    #particles-js canvas {
      display: block;
    }
  </style>
</head>
<body>
  <!-- 容器 -->
  <div id="particles-js"></div>

  <!-- 引入插件 -->
  <script src="js/particles.js"></script>
  <!-- 引入配置文件 -->
  <script src="js/app.js"></script>
</body>
</html>
```

> `app.js`

```js
particlesJS('particles-js',
  {
    "particles": {
      "number": {
        "value": 50,
        "density": {
          "enable": false,
          "value_area": 80
        }
      },
      "color": {
        "value": "#ccc"
      },
      "shape": {
        "type": "circle",
        "stroke": {
          "width": 0,
          "color": "#000000"
        },
        "polygon": {
          "nb_sides": 5
        },
        "image": {
          "src": "img/github.svg",
          "width": 100,
          "height": 100
        }
      },
      "opacity": {
        "value": 1,
        "random": false,
        "anim": {
          "enable": false,
          "speed": 1,
          "opacity_min": 0.1,
          "sync": false
        }
      },
      "size": {
        "value": 2,
        "random": true,
        "anim": {
          "enable": false,
          "speed": 40,
          "size_min": 0.1,
          "sync": false
        }
      },
      "line_linked": {
        "enable": true,
        "distance": 100,
        "color": "#ccc",
        "opacity": 0.8,
        "width": 1
      },
      "move": {
        "enable": true,
        "speed": 5,
        "direction": "none",
        "random": false,
        "straight": false,
        "out_mode": "out",
        "attract": {
          "enable": false,
          "rotateX": 600,
          "rotateY": 1200
        }
      }
    },
    "interactivity": {
      "detect_on": "canvas",
      "events": {
        "onhover": {
          "enable": false,
          "mode": "repulse"
        },
        "onclick": {
          "enable": false,
          "mode": "push"
        },
        "resize": true
      },
      "modes": {
        "grab": {
          "distance": 400,
          "line_linked": {
            "opacity": 1
          }
        },
        "bubble": {
          "distance": 400,
          "size": 40,
          "duration": 2,
          "opacity": 8,
          "speed": 3
        },
        "repulse": {
          "distance": 200
        },
        "push": {
          "particles_nb": 4
        },
        "remove": {
          "particles_nb": 2
        }
      }
    }
  }
);
```