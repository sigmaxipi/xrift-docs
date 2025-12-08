---
sidebar_position: 1
---

# 最初のワールドを作成する

このチュートリアルでは、XRift を使ってワールドを作成します。

## 前提条件

- Node.js 18.0.0 以上
- XRift CLI がインストール済み

## Step 1: プロジェクトの作成

新しいワールドプロジェクトを作成します：

```bash
xrift create my-first-world
cd my-first-world
```

## Step 2: 開発サーバーの起動

```bash
npm run dev
```

ブラウザで `http://localhost:5173` を開きます。

## Step 3: プロジェクト構成

作成されたプロジェクトは以下のような構成になっています：

```
my-first-world/
├── src/
│   ├── World.tsx        # メインのワールドコンポーネント
│   └── components/      # カスタムコンポーネント
├── public/              # アセット（モデル、テクスチャなど）
├── package.json
├── tsconfig.json
└── vite.config.ts
```

## Step 4: ワールドの編集

`src/World.tsx` を編集してワールドをカスタマイズします。

### 4.1 オブジェクトの追加

シンプルなキューブを追加します：

```tsx
export function World() {
  return (
    <>
      {/* ライティング */}
      <ambientLight intensity={0.5} />
      <directionalLight position={[10, 10, 5]} intensity={1} />

      {/* 地面 */}
      <mesh rotation={[-Math.PI / 2, 0, 0]} position={[0, 0, 0]}>
        <planeGeometry args={[20, 20]} />
        <meshStandardMaterial color="#444" />
      </mesh>

      {/* キューブを追加 */}
      <mesh position={[0, 0.5, -2]}>
        <boxGeometry args={[1, 1, 1]} />
        <meshStandardMaterial color="hotpink" />
      </mesh>
    </>
  );
}
```

### 4.2 アニメーションの追加

キューブを回転させてみましょう：

```tsx
import { useFrame } from '@react-three/fiber';
import { useRef } from 'react';
import type { Mesh } from 'three';

function RotatingCube() {
  const meshRef = useRef<Mesh>(null);

  useFrame((_, delta) => {
    if (meshRef.current) {
      meshRef.current.rotation.y += delta;
    }
  });

  return (
    <mesh ref={meshRef} position={[0, 0.5, -2]}>
      <boxGeometry args={[1, 1, 1]} />
      <meshStandardMaterial color="hotpink" />
    </mesh>
  );
}
```

### 4.3 インタラクションの追加

クリック可能なオブジェクトを追加します：

```tsx
import { Interactable } from '@xrift/world-components';

function InteractiveButton() {
  const handleInteract = () => {
    console.log('ボタンがクリックされました！');
  };

  return (
    <Interactable id="my-button" onInteract={handleInteract}>
      <mesh position={[2, 0.5, -2]}>
        <boxGeometry args={[0.5, 0.5, 0.5]} />
        <meshStandardMaterial color="skyblue" />
      </mesh>
    </Interactable>
  );
}
```

### 4.4 状態の同期

`useInstanceState` を使うと、ワールド内の全ユーザー間で状態を同期できます：

```tsx
import { useInstanceState, Interactable } from '@xrift/world-components';

function SyncedCounter() {
  const [count, setCount] = useInstanceState('counter', 0);

  return (
    <Interactable id="counter-button" onInteract={() => setCount(count + 1)}>
      <mesh position={[0, 1, -3]}>
        <boxGeometry args={[1, 1, 1]} />
        <meshStandardMaterial color={count % 2 === 0 ? 'green' : 'red'} />
      </mesh>
    </Interactable>
  );
}
```

## Step 5: ビルドとデプロイ

プロダクションビルドを作成します：

```bash
npm run build
```

XRift プラットフォームにアップロード：

```bash
xrift upload world
```

## 次のステップ

- [World Components](/world-components/overview) で利用可能なコンポーネントを確認
- [CLI コマンド](/cli/commands) で利用可能なコマンドを確認
