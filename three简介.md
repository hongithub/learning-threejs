# learning-threejs
threejs的学习
1.创建一个基本的场景渲染器：
function init(){
  //设置一个场景
  var scene = new THREE.Scene();
  //设置相机:
    //横纵比例设置
    var win_w = window.innerWidth;
    var win_h = window.innerHeight;
    var fx = win_w/win_h;
  var camera = new THREE.PerspectiveCamera(70,fx,0.1,1000);
  camera.position.x = -30;
  camera.position.y = 20;
  camera.position.z = 20;
  camera.lookat(scene.position);
  /*
    这里你可以添加其他的任何three.js相关物体demo
    eg:
      /*创建一个球体*/
		var sphereG = new THREE.SphereGeometry(4,10,10);
		var sphereM  =new THREE.MeshBasicMaterial({color:0x7777ff,wireframe:true});
		var o_sphere = new THREE.Mesh(sphereG,sphereM);
		scene.add(o_sphere);
		o_sphere.position.x = 20;
		o_sphere.position.y = 4;
		o_sphere.position.z = 2;
  */
  
  
  //设置渲染器：
  var renderer = new THREE.WebGLRenderer();
  renderer.setClearColor(new THREE.Color(0xeeeeee));
  renderer.setSize(win_w,win_h);
  
  ////把渲染器加入指定DOM中
  document.getElementById('output').appendChild(renderer,domElement);
  renderer.render(scene,camera);

}
window.onload = init;

解:
new THREE.Scene()==>设置一个场景
new THREE.PerspectiveCamera(70,fx,0.1,1000)==>设置一个远景透视相机
    PerspectiveCamera( fov, aspect, near, far )
    fov — 相机视锥体垂直视角
    aspect — 相机视锥体宽高比
    near — 相机视锥体近裁剪面
    far — 相机视锥体远裁剪面
new THREE.WebGLRenderer()==>设置渲染器为WebGL的渲染器
    .setClearColor(new THREE.Color(0xeeeeee))==>设置渲染器的渲染时的背景色
    .setSize(win_w,win_h)==>设置渲染器的大小
    document.getElementById('output').appendChild(renderer,domElement);==>挂载到dom元素上
    renderer.render(scene,camera)==render方法开始执行渲染开始带页面
    
new THREE.MeshBasicMaterial({color:0xff0000,wireframe:false})==>材质的设置
    .color==材质颜色的设置
    .wireframe:true/false==>物体材质表现true为实物全显，false为以线的描述显示；
new THREE.Mesh（gemotry,material）==>创建一个网格物体
    .position.x==设置物体的x位置
    .position.y==设置物体的y位置
    .position.z==设置物体的z位置
scene.add(obj)==>把创建的物体加入场景中



2.阴影的设置
  renderer.shadowMapEnabled = true/false===>渲染器开启阴影设置
  mesh.castShadow=true/false==>mesh产生阴影
  mesh.receiveShadow=true/false ==mesh接受阴影
  
3.动画的实现：实例
  requestAnimationFrame(renderScene);函数的使用；
  //设置变化的参数
  var step = 0;
  renderScene();
  function renderScene(){
    // rotate the cube around its axes
            cube.rotation.x += 0.02;
            cube.rotation.y += 0.02;
            cube.rotation.z += 0.02;

            // bounce the sphere up and down
            step += 0.01;
            sphere.position.x = 20 + ( 10 * (Math.cos(step)));
            sphere.position.y = 2 + ( 10 * Math.abs(Math.sin(step)));

            // render using requestAnimationFrame
            requestAnimationFrame(renderScene);
            renderer.render(scene, camera);
    
  }


4.窗口改变时对渲染器的实时设置
  // listen to the resize events
    window.addEventListener('resize', onResize, false);
    function onResize() {
        camera.aspect = window.innerWidth / window.innerHeight;
        camera.updateProjectionMatrix();
        renderer.setSize(window.innerWidth, window.innerHeight);
    }
    
