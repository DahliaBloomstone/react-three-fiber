# react-three-fiber

# 3D APPS WITH REACT THREE FIBER 
Some helpful notes! 

Three.js is a library that makes it easier to create 3D graphics in the browser, it uses a canvas + WebGL to display the 3D models and animations, you can learn more here.

react-three-fiber reduces the time spent on animations because of its reusable components, binding events and render loop. 

1. Create React App
2. Install dependencies: yarn add @react-spring/core react-spring react-three-fiber
3. also: three
4. create a new component: box.js

Bunch of hooks: Spring animates the rotation and scale of the boxes. 
```
import React, { useState, useEffect, useRef } from 'react' 
import { useSpring } from '@react-spring/core'
import { a } from "@react-spring/three" 

```


1. Down here what is happening: array of x,y,andz coordinates. 
2. It will hold the state. 
3. Define the spring and specify the parameters of the animation. 
4. Define the layout (rotation, scale)
5. Render the box buffer geometry, the size of the cube. 
6. Attach the material (mesh standard material) 
```
export const Box = ({ position }) => {
    const [ active, setActive] = useState(0)
    const activeRef = useRef(active)
    activeRef.current = active
  
    useEffect(() => {
      let timeout
      const toggleActive = () => {
        timeout = setTimeout(() => {
          setActive(Number(!activeRef.current))
          toggleActive()
        }, Math.random() * 2000 + 1000)
      }
      toggleActive()
      return () => {
        clearTimeout(timeout)
      }
    }, [])
  
    const { spring } = useSpring({
      spring: active,
      config: { mass: 5, tension: 400, friction: 50, precision: 0.0001 }
    })
  
    const scale = spring.to([0, 1], [1, 2])
    const rotation = spring.to([0, 1], [0, Math.PI])
    const color = spring.to([0, 1], ["#50c878", "#e45858"])
  
    return (
      <a.mesh
        rotation-y={rotation}
        scale-x={scale}
        scale-y={scale}
        scale-z={scale}
        position={position}
      >
        <boxBufferGeometry attach="geometry" args={[1, 1, 1]}/>
        <a.meshStandardMaterial roughness={0.5} attach="material" color={color}/>
      </a.mesh>
    )
  }
```

TOGGLE ACTIVE: must call for the boxes to be able to animate. 

Define an affect that will trigger the state? 
useEffect. It returns the function. 

export Box.js and import it in app.js

ambientLight, pointLight, camera and canvas:
* the canvas: is used to draw the graphics on the browser.
* ambientLight: This is used to light all objects in a scene or model equally, it accepts props such as the intensity of the light.
* pointLight: This works similar to the light of a light bulb, light is emitted from a single point to all directions, this will be necessary for the active state of our application.


```
import React from "react";
import { Canvas } from "react-three-fiber";
import { Box } from "./Box";

function App() {
  return (
    <Canvas camera={{ position: [-10, 10, 10], fov: 35 }}>
      <ambientLight />
      <pointLight position={[-10, 10, -10]} castShadow />
      {[-3, 0, 3].map((x) =>
        [-3, 0, 3].map((z) => <Box position={[x, 0, z]} />)
      )}
    </Canvas>
  );

}

export default App;
```

helpful article; https://www.smashingmagazine.com/2020/11/threejs-react-three-fiber/


# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `yarn start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `yarn test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `yarn build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `yarn eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `yarn build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)
