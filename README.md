<h1 align="center">VRMKit</h1>

<h5 align="center">VRM loader and VRM renderer</h5>

<div align="center">
  <a href="https://app.bitrise.io/app/efaa4b22f111455d">
    <img src="https://github.com/tattn/VRMKit/actions/workflows/ci.yml/badge.svg" />
  </a>
  <a href="./LICENSE">
    <img src="https://img.shields.io/badge/license-MIT-green.svg?style=flat-square" alt="license:MIT" />
  </a>
</div>

<br />

<div>
<img src="https://github.com/tattn/VRMKit/raw/main/.github/demo.jpg" width="300px" alt="demo" />
<img src="https://github.com/tattn/VRMKit/raw/main/.github/demo2.gif" width="300px" alt="demo" />
</div>

For "VRM", please refer to [this page](https://dwango.github.io/en/vrm/).

## Features

- [x] Load VRM file
- [x] Render VRM models on SceneKit (experimental)
- [x] Face morphing (blend shape)
- [x] Bone animation (skin / joint)
- [x] Physics (spring bone)

# Requirements

- Swift 5.7+
- iOS 15.0+
- watchOS 8.0+ (Experimental)

# Installation

## Swift Package Manager

You can install this package with Swift Package Manager.

## Carthage & CocoaPods (Deprecated)

If you want to use these package managers, please use https://github.com/tattn/VRMKit/releases/tag/0.4.2

# Usage

## Load VRM

```swift
import VRMKit

let vrm = try VRMLoader().load(named: "model.vrm")
// let vrm = try VRMLoader().load(withUrl: URL(string: "/path/to/model.vrm")!)
// let vrm = try VRMLoader().load(withData: data)

// VRM meta data
vrm.meta.title
vrm.meta.author

// model data
vrm.gltf.jsonData.nodes[0].name
```

## Render VRM

```swift
import VRMKit
import VRMSceneKit

@IBOutlet weak var sceneView: SCNView!

let loader = try VRMSceneLoader(named: "model.vrm")
let scene: VRMScene = try loader.loadScene()
let node: VRMNode = scene.vrmNode

sceneView.scene = scene
```

### Blend shapes

<img src="https://github.com/tattn/VRMKit/raw/main/.github/alicia_joy.png" width="100px" alt="joy" />

```swift
node.setBlendShape(value: 1.0, for: .preset(.joy))
```

<img src="https://github.com/tattn/VRMKit/raw/main/.github/alicia_angry.png" width="100px" alt="angry" />

```swift
node.setBlendShape(value: 1.0, for: .preset(.angry))
```

<img src="https://github.com/tattn/VRMKit/raw/main/.github/alicia_><.png" width="100px" alt="><" />

```swift
node.setBlendShape(value: 1.0, for: .custom("><"))
```

### Bone animation

<img src="https://github.com/tattn/VRMKit/raw/main/.github/alicia_humanoid.png" width="200px" alt="Humanoid" />

```swift
node.setBlendShape(value: 1.0, for: .preset(.fun))
node.humanoid.node(for: .neck)?.eulerAngles = SCNVector3(0, 0, 20 * CGFloat.pi / 180)
node.humanoid.node(for: .leftShoulder)?.eulerAngles = SCNVector3(0, 0, 40 * CGFloat.pi / 180)
node.humanoid.node(for: .rightShoulder)?.eulerAngles = SCNVector3(0, 0, 40 * CGFloat.pi / 180)
```

### Read the thumbnail image

```swift
let loader = try VRMSceneLoader(named: "model.vrm")
let image = try loader.loadThumbnail()
```

# ToDo
- [ ] VRM shaders support
- [ ] Improve rendering quality
- [ ] Animation support
- [ ] VRM editing function
- [ ] GLTF renderer support

# Contributing

1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :D

## Support this project

Donating to help me continue working on this project.

[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://paypal.me/tattn/)

# License

VRMKit is released under the MIT license. See LICENSE for details.

# Author
Tatsuya Tanaka

<a href="https://twitter.com/tanakasan2525" target="_blank"><img alt="Twitter" src="https://img.shields.io/twitter/follow/tanakasan2525.svg?style=social&label=Follow"></a>
<a href="https://github.com/tattn" target="_blank"><img alt="GitHub" src="https://img.shields.io/github/followers/tattn.svg?style=social"></a>

