# Loading models with Three React Fibar

## Fixing the example code to use a component with a model multiple times

The [example code in the documenation](https://docs.pmnd.rs/react-three-fiber/tutorials/loading-models#loading-gltf-models) can load a model only once.
It will provide the model as react component, but once you try to use the component multiple times in the same scene, then it will be displayed only once.

It will work if you clone the loaded scene instead of only inserting it:

```JavaScript
function Scene() {
  const gltf = useLoader(GLTFLoader, '/Poimandres.gltf')
  return (
    <Suspense fallback={null}>
      <primitive object={gltf.scene.clone()} />
    </Suspense>
  )
}
```

## Loading `.glb` models

You can use the `GLTFLoader` loader to load `.glb` files.
