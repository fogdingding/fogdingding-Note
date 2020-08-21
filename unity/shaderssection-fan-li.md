---
description: >-
  Material (Texture +
  Shader)。Shader即著色器，是一款執行在GPU上的程式，用來對三維物體進行著色處理、光與影的計算、紋理顏色的呈現等，從而將遊戲引擎中的一個個作為抽象的幾何資料存在的模型、場景和特效，以和真實世界類似的光與影的形式呈現在玩家的眼中。
---

# Shaders-Section範例

#### 創建物件

建立完Unity的一個3D範例後，進入至Assets資料夾內後。

```text
.
├── Scenes
│   ├── SampleScene.unity
│   └── SampleScene.unity.meta
└── Scenes.meta
```

在此資料夾內新增以下檔案

* New Material.mat
* NewUnlitShader.shader

![&#x65B0;&#x589E;New Material.mat](../.gitbook/assets/new-material.png)

![&#x65B0;&#x589E;NewUnlitShader.shader](../.gitbook/assets/newunlitshader.png)

在SampleScene.unity內部新增一個3D Object Cube

![&#x65B0;&#x589E;Cube](../.gitbook/assets/new-cube.png)

#### 編輯程式碼

於NewUnlitShader.shader修改程式碼

```text
Shader "Custom/NewUnlitShader" {
 
    Properties {
        _Color1 ("Outside color", Color) = (1.0, 1.0, 1.0, 1.0)
        _Color2 ("Section color", Color) = (1.0, 1.0, 1.0, 1.0)
        _EdgeWidth ("Edge width", Range(0.9, 0.1)) = 0.9
        _Val ("Height value", float) = 0
    }
 
    SubShader {
        Tags { "Queue"="Geometry" }
 
        //  PASS 1
        CGPROGRAM
        #pragma surface surf Standard
 
        struct Input {
            float3 worldPos;
        };
 
        fixed4 _Color1;
        float _Val;
 
        void surf(Input IN, inout SurfaceOutputStandard o)
        {
            if(IN.worldPos.y > _Val)
                discard;
            o.Albedo = _Color1;
        }
 
        ENDCG
 
        //  PASS 2
        Pass {
 
            Cull Front
 
            CGPROGRAM
            #pragma vertex vert
            #pragma fragment frag
            #include "UnityCG.cginc"
 
            struct v2f {
                float4 pos : SV_POSITION;
                float4 worldPos : TEXCOORD0;
            };
 
            v2f vert(appdata_base v)
            {
                v2f o;
                o.pos = mul(UNITY_MATRIX_MVP, v.vertex);
                o.worldPos = mul(unity_ObjectToWorld, v.vertex);
                return o;
            }
 
            fixed4 _Color2;
            float _Val;
 
            fixed4 frag(v2f i) : SV_Target {
                if(i.worldPos.y > _Val)
                    discard;
 
                return _Color2;
            }
 
            ENDCG
        }
 
        //  PASS 3
        Pass {
            CGPROGRAM
            #pragma vertex vert
            #pragma fragment frag
            #include "UnityCG.cginc"
 
            struct v2f {
                float4 pos : SV_POSITION;
                float4 worldPos : TEXCOORD0;
            };
 
            float _EdgeWidth;
 
            v2f vert(appdata_base v)
            {
                v2f o;
                v.vertex.xyz *= _EdgeWidth;
                o.pos = mul(UNITY_MATRIX_MVP, v.vertex);
                o.worldPos = mul(unity_ObjectToWorld, v.vertex);
                return o;
            }
 
            fixed4 _Color2;
            float _Val;
 
            fixed4 frag(v2f i) : SV_Target {
                if(i.worldPos.y > _Val)
                    discard;
 
                return _Color2;
            }
 
            ENDCG
        }
 
        //  PASS 4
        Cull Front
 
        CGPROGRAM
        #pragma surface surf Standard vertex:vert
        struct Input {
            float3 worldPos;
        };
 
        float _EdgeWidth;
 
        void vert(inout appdata_base v)
        {
            v.vertex.xyz *= _EdgeWidth;
        }
 
        fixed4 _Color1;
        float _Val;
 
        void surf(Input IN, inout SurfaceOutputStandard o)
        {
            if(IN.worldPos.y > _Val)
                discard;
 
            o.Albedo = _Color1;
        }
 
        ENDCG
    }
}
```

#### 物件指向

* 將NewUnlitShader.shader指向New Material.mat
* 將New Material.mat指向Cube

備註：拖拉檔案至目標即可自動指向。

完成會如下圖

![NewUnlitShader.shader&#x6307;&#x5411;New Material.mat&#x5F8C;](../.gitbook/assets/section-material.png)

![&#x5C07;New Material.mat&#x6307;&#x5411;Cube&#x5F8C;](../.gitbook/assets/section-cube.png)

點選Cube並查看右下角即可進行拖拉改變Cube的切面狀況。

![&#x4FEE;&#x6539;Cube&#x7684;Shader&#x7684;&#x53C3;&#x6578;](../.gitbook/assets/section-material-change.png)

![&#x4FEE;&#x6539;&#x5F8C;&#x7684;Cube&#x72C0;&#x6CC1;](../.gitbook/assets/section_cube-new.png)

#### 資料來源

* [Shaders Laboratory](https://www.youtube.com/channel/UCDk9-aPr8zQzwi4ylnuoJ6w)[Section Shaders](https://www.youtube.com/watch?v=AhC6ueyny2I)
* [write Shaders](https://www.youtube.com/watch?v=bR8DHcj6Htg)
* [sample](https://www.shadertoy.com/results?query=&sort=popular)
* [shaders lab](http://www.shaderslab.com/index.html)

