# THREEjs必备组件
## 场景
空间舞台
```javascript
    const scene = new THREE.Scene()
```
**api**：
![690022a9aaed6b7b929405efa54d298a.png](evernotecid://CF19D477-EF20-4B48-B9E6-CD9CEEA65F1B/appyinxiangcom/23645429/ENResource/p2)

**属性**：
- fog：设置场景的雾化效果（可定义雾化位置）-越远的地方越模糊
- overrideMaterial：是场景中所有的物体都使用相同的材质--一般用于测试
- children：返回场景所有对象的列表--包括相机合光源对象

## 相机
决定哪些东西将被显示到屏幕上
角度
近距点
远距点
```javascript
    // 定义一个透视相机(视角，长宽比，近距点，远距点)
    const camera = new THREE.PerspectiveCamera(50, window.innerWidth / window.innerHeight, 0.1, 1000)
    // 相机位置
    camera.position.set(-30,40,30)
    // 看向
    camera.lookAt(scene.position)
```
## 渲染器
渲染出你精心制作的场景
```javascript
    // 创建一个WebGL渲染器
    const renderer = new THREE.WebGLRenderer()
    // 设置用于清屏的背景色
    renderer.serClearColor( new THREE.Color(0xefefef,1.0))
    // 定义renderer绘制区域
    renderer.setSize( window.innerWidth, window.innerHeight)
    // 开启阴影支持
    renderer.shadowMapEnabled = true
    // 渲染
    renderer.render(scene,camera)

```
## 光源
生成阴影与改变物体表面显示效果
环境光
点光源--聚光灯
背面光
正面光
```javascript
    // 创建环境光
    const ambientLight = new THREE.AmbientLight(0x0c0c0c)
    // 放入场景
    scene.add(ambientLight)
    // 创建点光源
    const spotLight = new THREE.SpotLight(0xffffff)
    // 点光源位置
    spotLight.position.set(-40,60,-10)
    // 放入场景
    scene.add(spotLight)
```
## 物体
相机透视图里主要的渲染对象

### 平面
舞台地面
```javascript
    // 平面几何对象
    const planeGeometry = new THREE.PlaneGeometry(70,50,1,1)
    // 创建平面材质
    const planeMeterail = new THREE.MeshLamberMaterail({color:0xcccccc})
    // 创建平面物体
    const plane = new THREE.Mesh(planeGeometry,planeMeterail)
    // 平面旋转
    plane.rotation.x=-.5*Math.PI
    // 平面位置
    plane.position.x=0
    plane.position.y=0
    plane.position.z=0
    // 放入场景
    scene.add(plane)
```
### 创建立方体
```javascript
    // 定义一个随机位置的立方体
    function addCube(){
        const cubeGeometry = new THREE.BoxGeometry(5,5,5)
        const cubeMaterial = new THREE.MeshLamberMaterial({color:0xcccfff})
        const cube = new THREE.Mesh(cubeGeometry,cubeMaterial)
        cube.position.x=-30+Math.round(Math.random()*PlaneGeometry.parameters.width)
        cube.position.y=Math.round(Math.random()*5)
        cube.position.z=-20+Math.round(Math.random()*PlaneGeometry.parameters.height)
       scene.add(cube)
    }
    // render函数
    function render(){
        addCube()
        renderer.render(scene,camera)
        // 循环动画
        requestAnimationFrame(render)
    }
    render()
```
