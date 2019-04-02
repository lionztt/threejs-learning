## 3D对象 = 网格+几何体
THREE.Geometry是所有几何对象的基类
- geometry.vertices表示几何体顶点数组
- geometry.faces表示几何体的面数组
## 网格对象 = 材质+3D对象
![70221a0de813198c663ee12faff4c666.png](evernotecid://CF19D477-EF20-4B48-B9E6-CD9CEEA65F1B/appyinxiangcom/23645429/ENResource/p3)

```javascript
    const scene = new THREE.Scene()
    // 人眼的视角是120度，但我们在做时一般小于60度
    const camera = new THREE.PerspectiveCamera(45,window.innerWidth/window.innerHeight,0.1,1000)
    camera.position.set(-20,25,20)
    camera.lookAt(scene.position)

    const clearColor = new THREE.Color(0xeeeeee,1.0)
    const renderer = new THREE.WebGLRenderer(clearColor)
    renderer.setSize(window.innerWidth,window.innerHeight)
    renderer.shadoqMapEnabled = true
    const plane = new THREE.Mesh(new THREE.PlaneGeometry(60,40,1,1),new THREE.MeshLamberMaterial({color:0xffffff}))
    plane.rotation.x=-.5*Math.PI
    plane.position.set(0,0,0)
    scene.add(plane)

    const spotLight=new THREE.SpotLight(0xffffff)
    spotLight.position.set(-40,60,10)
    spotLight.castShadow=true
    scene.add(spotLight)

    // 长方体8个顶点坐标
    const vertices = [
        new THREE.Vector3(1,3,1),
        new THREE.Vector3(1,3,-1),
        new THREE.Vector3(1,-1,1),
        new THREE.Vector3(1,-1,-1),
        new THREE.Vector3(-1,3,-1),
        new THREE.Vector3(-1,3,1),
        new THREE.Vector3(-1,-1,-1),
        new THREE.Vector3(-1,-1,1)
    ]

    // 长方体面数组(面是由点的索引构成--3点成三角形（两个为一组面）)
    const faces = [
        new THREE.Face3(0,2,1),
        new THREE.Face3(2,3,1),

        new THREE.Face3(4,6,5),
        new THREE.Face3(6,7,5),

        new THREE.Face3(4,5,1),
        new THREE.Face3(5,0,1),

        new THREE.Face3(7,6,2),
        new THREE.Face3(6,3,2),

        new THREE.Face3(5,7,0),
        new THREE.Face3(7,2,0),

        new THREE.Face3(1,3,4),
        new THREE.Face3(3,6,4)
    ]

    const geometry = new THREE.Geometry()
    geometry.vertices = vertices
    geometry.faces = faces
    // 面的标准化处理
    geometry.computeFaceNormals()
    // 综合材质
    const materials=[new THREE.MeshLamberMatrial({opacity:0.5,color:0x44ff44,transparent:true}),
    new THREE.MeshBasicMaterial({color:0x000000,wireframe:true})]
    const mesh = THREE.SceneUtils.createMultiMaterialObject(geometry.materials)
    mesh.children.forEach(function(e){
        e.castShadow = true
    })
    scene.add(mesh)
    document.body.appendChild(renderer.domElement)
    renderer.render(scene,camera)

```