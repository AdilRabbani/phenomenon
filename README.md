
# Phenomenon

Phenomenon is a very small, low-level WebGL library that provides the essentials to deliver a high performance experience. Its core functionality is built around the idea of moving *millions of particles* around using the power of the GPU.

#### Features:

- Small in size, no dependencies
- GPU based for high performance
- Low-level & highly configurable
- Helper functions with options
- Add & destroy instances dynamically

*Want to see some magic right away? Have a look <a href="https://codepen.io/collection/AOpMrm/">here</a>!*

## Install

```
$ npm install --save phenomenon
```

## Usage

```js
// Import the library
import Phenomenon from 'phenomenon';

// Create a renderer
const phenomenon = new Phenomenon(options);

// Add an instance
phenomenon.add("particles", options);
```

> For a better understanding of how to use the library, read along or have a look at the demo!

## API

### Phenomenon(options)

Returns an instance of Phenomenon.

> Throughout this documentation we'll refer to an instance of this as `renderer`.

#### options.canvas
Type: `HTMLElement` <br/>
Default: `document.querySelector('canvas')` <br/>

The element where the scene, with all of its instances, will be rendered to. The provided element has to be `<canvas>` otherwise it won't work.

#### options.context
Type: `Object`<br/>
Default: `{}`<br/>

Overrides that are used when getting the WebGL context from the canvas. The library overrides two settings by default.

| Name      | Default | Description                                                                                                                             |
| --------- | --------| --------------------------------------------------------------------------------------------------------------------------------------- |
| Alpha     | `false` | Setting this property to `true` will result in the canvas having a transparent background. By default clearColor is used instead.   |
| Antialias | `false` | Setting this property to `true` will make the edges sharper, but could negatively impact performance. See for yourself if it's worth it! |

> Read more about all the possible overrides on <a href="https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/getContext">MDN</a>.

#### options.settings
Type: `Object`<br/>
Default: `{}`<br/>

@TODO
Overrides that can be used to alter the behaviour of the experience.

| Name                                     | Value      | Default     | Description                                                                 |
| ---------------------------------------- | ---------- | ----------- | --------------------------------------------------------------------------- |
| devicePixelRatio                         | `number`   | `1`         | The resolution multiplier by which the scene is rendered relative to the canvas' resolution. Use `window.devicePixelRatio` for the highest possible quality, `1` for the best performance. |
| clearColor                               | `array`    | `[1,1,1,1]` | The color in `rgba` that is used as the background of the scene. |
| position                                     | `number`   | `{x:0,y:0,z:2}`         | The distance in 3D space between the center of the scene and the camera. |
| shouldRender                             | `boolean`  | `true`      | A boolean indicating whether the scene should start rendering automatically. |
| uniforms                                 | `object`   | `{}`        | Shared values between all instances that can be updated at any given moment. By default this feature is used to render all the instances with the same `uProjectionMatrix`, `uModelMatrix` and `uViewMatrix`. It's also useful for moving everything around with the same progress value; `uProgress`. |
| willRender(renderer) didRender(renderer) | `function` | `undefined` | A render hook that is invoked every frame before / after the scene is rendered to the screen. Use this to update `renderer.uniforms`. |

### .resize()

Update all values that are based on the dimensions of the canvas to make it look good on all screen sizes.

### .toggle(shouldRender)

Toggle the rendering state of the scene. When shouldRender is false `requestAnimationFrame` is disabled so no resources are used.

#### shouldRender
Type: `Boolean` <br/>
Default: `undefined` <br/>

An optional boolean to set the rendering state to a specific value. Leaving this value empty will result in a regular boolean switch.

### .add(key, settings)

This function is used to add instances to the renderer. These instances can be as *simple* or *complex* as you'd like them to be. There's no limit to how many of these you can add. Make sure they all have a different key!

#### key
Type: `String`<br/>
Default: `undefined`<br/>

Every instance should have a unique name. This name can also be used to destroy the instance specifically later.

#### settings
Type: `Object`<br/>
Default: `{}`<br/>

An object containing overrides for parameters that are used when getting the WebGL context from the canvas.

| Name        | Value      | Default  | Description                                                                 |
| ----------- | ---------- | -------- | --------------------------------------------------------------------------- |
| attributes  | `array`    | -        | Values used in the program that are stored once, directly on the GPU.       |
| uniforms    | `object`   | `{}`     | Values used in the program that can be updated on the fly.                  |
| vertex      | `string`   | -        | The vertex shader is used to position the geometry in 3D space.             |
| fragment    | `string`   | -        | The fragment shader is used to provide the geometry with color or texture.  |
| multiplier  | `number`   | -        | The amount of duplicates that will be created for the same instance.        |
| geometry    | `object`   | `{}`     | Vertices (and optional normals) of a model.                                 |
| modifiers   | `object`   | `{}`     | Modifiers to alter the attributes data on initialize.                       |
| willRender  | `function` | `null`   | A render hook that is invoked every frame before the instance is rendered.  |
| didRender   | `function` | `null`   | A render hook that is invoked every frame after the instance is rendered.   |

> Note: Less instances with a higher multiplier will be faster than more instances with a lower multiplier!

### .remove(key)

Remove an instance from the scene (and from memory) by its key.

### .destroy()

Remove all instances and the renderer itself. The canvas element will remain in the DOM.

## Examples

1. <a href="https://codepen.io/cvaneenige/pen/odpVPW">Particles</a>
2. <a href="https://codepen.io/cvaneenige/pen/GdGpaN">Types</a>
3. <a href="https://codepen.io/cvaneenige/pen/Lmrzmd">Transition</a>
4. <a href="https://codepen.io/cvaneenige/pen/zjaydg">Easing</a>
5. <a href="https://codepen.io/cvaneenige/pen/wjXVgr">Shapes</a>
6. <a href="https://codepen.io/cvaneenige/pen/MGBZpB">Instances</a>
7. <a href="https://codepen.io/cvaneenige/pen/LmXWeM">Movement</a>

## Contribute

Are you excited about this library and have interesting ideas on how to improve it? Please tell me or contribute directly! 🙌

```
npm install > npm run demo > http://localhost:8080
```

## License

MIT © <a href="https://use-the-platform.com">Colin van Eenige</a>
