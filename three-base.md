

## 绘制旋转的立方体
---

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>three.js-绘制旋转的立方体</title>
  <style>
    * {
      margin: 0;
      padding: 0;
    }
    canvas {
      display: block;
    }
  </style>
</head>
<body>
  <script src="https://cdn.bootcss.com/three.js/92/three.min.js"></script>
  <script>
    // 设置宽高
    const W = window.innerWidth
    const H = window.innerHeight

/* 初始化 */

    // 场景
    const scene = new THREE.Scene()
    // 相机 (视角, 窗口横纵比, 近平面, 远平面)
    const camera = new THREE.PerspectiveCamera(45, W / H, 1, 1000)
    // 渲染器 (将场景渲染到屏幕上 )
    const renderer = new THREE.WebGLRenderer()
    // 设置渲染器的颜色
    renderer.setClearColor('#d0efb5')
    // 设置渲染器的大小
    renderer.setSize(W, H)
    // 添加到body中
    document.body.appendChild(renderer.domElement)

/* 初始化立方体 */

    // 定义一个几何体 (长, 宽, 高)
    const geometry = new THREE.CubeGeometry(1, 1, 1)
    // 定义材质
    const material = new THREE.MeshBasicMaterial({color: '#2aa9d2'})
    // 创建模型
    const cube = new THREE.Mesh(geometry, material)
    // 调整相机距离
    camera.position.z = 5
    // 把模型添加到场景中
    scene.add(cube)

/* 渲染立方体 */

    function render() {
      cube.rotation.x += 0.02
      cube.rotation.y += 0.01
      // 渲染场景和相机
      renderer.render(scene, camera)
      // 循环调用render函数
      requestAnimationFrame(render)
    }

    render()
  </script>
</body>
</html>
```

<br>

## 绘制一条线
---

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>three.js-绘制一条线</title>
        <script src="https://cdn.bootcss.com/three.js/92/three.min.js"></script>
        <style type="text/css">
          * {
            margin: 0;
            padding: 0;
          }
          canvas {
            display: block;
          }
            div#canvas-frame {
                width: 100%;
                height: 600px;
            }

        </style>
        <script>
            var renderer;
            function initThree() {
                width = document.getElementById('canvas-frame').clientWidth;
                height = document.getElementById('canvas-frame').clientHeight;
                renderer = new THREE.WebGLRenderer({
                    antialias : true
                });
                renderer.setSize(width, height);
                document.getElementById('canvas-frame').appendChild(renderer.domElement);
                renderer.setClearColor('#e4d1d3', 1.0);
            }

            var camera;
            function initCamera() {
                camera = new THREE.PerspectiveCamera(45, width / height, 1, 10000);
                camera.position.x = 0;
                camera.position.y = 1000;
                camera.position.z = 0;
                camera.up.x = 0;
                camera.up.y = 0;
                camera.up.z = 1;
                camera.lookAt(0, 0, 0);
            }

            var scene;
            function initScene() {
                scene = new THREE.Scene();
            }

            var light;
            function initLight() {
                light = new THREE.DirectionalLight(0xFF0000, 1.0, 0);
                light.position.set(100, 100, 200);
                scene.add(light);
            }

            var cube;
            function initObject() {

                var geometry = new THREE.Geometry();
                var material = new THREE.LineBasicMaterial( { vertexColors: true } );
                var color1 = new THREE.Color( 0x444444 ), color2 = new THREE.Color( 0xFF0000 );

                // 线的材质可以由2点的颜色决定
                var p1 = new THREE.Vector3( -100, 0, 100 );
                var p2 = new THREE.Vector3(  100, 0, -100 );
                geometry.vertices.push(p1);
                geometry.vertices.push(p2);
                geometry.colors.push( color1, color2 );

                var line = new THREE.Line( geometry, material, THREE.LineSegments)
                scene.add(line);
            }

            function threeStart() {
                initThree();
                initCamera();
                initScene();
                initLight();
                initObject();
                renderer.clear();
                renderer.render(scene, camera);
            }

        </script>
    </head>

    <body onload="threeStart();">
        <div id="canvas-frame"></div>
    </body>
</html>
```