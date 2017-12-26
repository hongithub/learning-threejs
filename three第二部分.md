# learning-threejs
threejs的学习
第二部分
阴影的设置：
renderer.shadowMapEnabled = true;==>渲染器开启阴影设置
obj.receiveShadow = true/false;==>接受阴影设置
obj.castShadow = true;==>产生阴影
位置的设置：
obj.position.set(x,y,z);在屏幕位置的设置x轴 y轴 z轴
obj.rotation.set(x,y,z);旋转角度的设置
obj.scale.set(x,y,z);缩放因子的设置

scene.traverse的方法：设置遍历每个子对象
  例子：
  // rotate the cubes around its axes
            scene.traverse(function (e) {
                if (e instanceof THREE.Mesh && e != plane) {

                    e.rotation.x += controls.rotationSpeed;
                    e.rotation.y += controls.rotationSpeed;
                    e.rotation.z += controls.rotationSpeed;
                }
            });
