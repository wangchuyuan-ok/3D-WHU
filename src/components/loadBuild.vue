<template>
    <canvas id="renderCanvas"></canvas>
</template>
  
<script>
import * as BABYLON from "babylonjs"
import 'babylonjs-loaders';
window.addEventListener('DOMContentLoaded', function () {
    var canvas = document.getElementById("renderCanvas"); // 获取到renderCanvas这个要素
    var engine = new BABYLON.Engine(canvas, true); // 在这里创建巴比伦引擎

    var createScene = function () {
        var scene = new BABYLON.Scene(engine);
        new BABYLON.HemisphericLight("light1", new BABYLON.Vector3(0, 1, 0), scene);
        var cam = new BABYLON.ArcRotateCamera("ArcRotateCamera", 100, -400, 500, new BABYLON.Vector3(-50, 1, 0), scene);
        cam.attachControl(canvas);
        var loader = new BABYLON.AssetsManager(scene);
        var position = 0;
        var pos = function (t) {
            t.loadedMeshes.forEach(function (m) {
                m.position.x -= position;
            });
            position += 1;
        };
        var bunny1 = loader.addMeshTask("XingZhengLou", "", "./data/", "XingZhengLou.gltf");
        var bunny2 = loader.addMeshTask("G-1-002", "", "./data/", "G-1-002.gltf");
        bunny1.onSuccess = pos;
        bunny2.onSuccess = pos;
        loader.onFinish = function () {
            engine.runRenderLoop(function () {
                scene.render();
            });
        };
        loader.load();

        return scene;
    };
    /*下面解释createScene()函数怎么用*/
    var scene = createScene(); // 首先调用它并赋值给一个变量
    // 注册一个渲染循环来重复渲染场景
    engine.runRenderLoop(function () {
        scene.render();
    });
    // 观察浏览器/画布的“resize”事件，也就是大小出现调整的事件
    window.addEventListener("resize", function () {
        engine.resize();
    });

});

export default {

}

</script>
  
<style>
#renderCanvas {
    width: 100%;
    height: 100%;
    touch-action: none;
}
</style>
  