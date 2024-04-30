#### 실습화면

![Animation](https://github.com/qkrgudals1030/Transformation/assets/50895124/de752d02-758e-461b-beab-4ce3b6161f5e)


### 소감

직접동작하는 웹기반 오브젝트를 유튜브 영상을 보면서 제작해보니 조금더 쉽게 오브젝트를 쉽게 배워볼 수 있었고 이런 오브젝트를 영상만보고 따라 만드는 것이 아닌 












### .jsx
```

import { OrbitControls } from "@react-three/drei"
import { useFrame } from "@react-three/fiber"
import { useRef } from "react"
import * as THREE from "three"

function MyElement3D(){
    const refMesh = useRef()
    useFrame((state, delta) => {
        refMesh.current.rotation.y += delta
    })
    return(
        <>
            <directionalLight position={[1, 1, 1]} />

            <axesHelper scale={10}/>
            <OrbitControls />

            <mesh ref={refMesh} 
                position-y={ 2 }
                rotation-z={ THREE.MathUtils.degToRad(45) }
                scale={ [2, 1, 1] }
            >
                <boxGeometry />
                <meshStandardMaterial color="#e67e22" 
                opacity={0.5} transparent={true}
                />
                <axesHelper/>


                <mesh
                scale={[0.1,0.1,0.1]}
                position-y={2}
                >
                    <sphereGeometry />
                    <meshStandardMaterial color ="red" />
                </mesh>

            </mesh>
        </>
    )
}

export default MyElement3D

```


