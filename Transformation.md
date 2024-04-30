#### 실습화면

![Animation](https://github.com/qkrgudals1030/Transformation/assets/50895124/de752d02-758e-461b-beab-4ce3b6161f5e)


![image](https://github.com/qkrgudals1030/Transformation/assets/50895124/b4057c9c-604d-4f4f-a3ff-bef2036cafb7)



### 소감

직접동작하는 웹기반 오브젝트를 유튜브 영상을 보면서 제작해보니 조금더 쉽게 오브젝트를 쉽게 배워볼 수 있었고 이런 오브젝트를 영상만보고 따라 만드는 것이 아닌 제가 만든 오브젝트들을 수정도 해보면서 코딩에 대한 실력을 늘릴수 있었고 또한 나중에 내주시는 저희가 직접만들어 보는 메타버스 프로젝트를 잘 만들어 낼수 있도록 연습을 해볼 수 있는 기회가 될 수 있었습니다. 잘 복습하여 좋은 결과물을 만들 수 있도록 잘 복습과 반복을 해보겠습니다. ai그래픽스 화이팅!!!






### 4.jsx
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
### 5.jsx
```
import { Box, OrbitControls } from "@react-three/drei"
import { useControls } from "leva"
import {useEffect, useRef} from "react"
import * as THREE from "three"

function MyElement3D(){
    const refMesh = useRef()
    const refWireMesh = useRef()

    const { xSize,ySize,zSize,xSegments,ySegments,zSegments } = useControls({
        xSize: {value: 1, min: 0.1, max: 5, step: 0.01 },
        ySize: {value: 1, min: 0.1, max: 5, step: 0.01 },
        zSize: {value: 1, min: 0.1, max: 5, step: 0.01 },
        xSegments: {value: 1, min: 1, max: 10, step: 1 },
        ySegments: {value: 1, min: 1, max: 10, step: 1 },
        zSegments: {value: 1, min: 1, max: 10, step: 1 },
    })


    useEffect(() => {
      refWireMesh.current.geometry = refMesh.current.geometry
    }, [xSize,ySize,zSize,xSegments,ySegments,zSegments])

    return(
        <>
        
            <OrbitControls />

           <ambientLight intensity={0.1}/>
           <directionalLight position={[2,1,3]} intensity={0.5}/>

            <mesh ref={refMesh}>
                <boxGeometry args={[xSize,ySize,zSize,xSegments,ySegments,zSegments]}/>
                <meshStandardMaterial color="#1abc9c" />
            </mesh>

            <mesh ref={refWireMesh}>
                <meshStandardMaterial emissive="yellow" wireframe={true} />
            </mesh>

        </>
    )
}

export default MyElement3D
```

