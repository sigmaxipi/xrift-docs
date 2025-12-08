---
sidebar_position: 2
---

# World Components 概要

xrift-world-components は、XRift ワールドを構築するための React コンポーネント・フックライブラリです。

## 特徴

- React Three Fiber ベース
- マルチユーザー状態同期
- TypeScript 完全サポート

## インストール

```bash
npm install @xrift/world-components
```

### ピア依存関係

以下のパッケージも必要です：

```bash
npm install react three @react-three/fiber @react-three/drei
```

## 基本的な使い方

```tsx
import { Interactable, useInstanceState } from '@xrift/world-components';

export function World() {
  const [count, setCount] = useInstanceState('counter', 0);

  return (
    <>
      <ambientLight />
      <Interactable id="button" onInteract={() => setCount(count + 1)}>
        <mesh>
          <boxGeometry />
          <meshStandardMaterial color={count % 2 === 0 ? 'hotpink' : 'skyblue'} />
        </mesh>
      </Interactable>
    </>
  );
}
```

## 提供されるもの

### コンポーネント

| コンポーネント | 説明 |
|--------------|------|
| `Interactable` | クリック可能なオブジェクトを作成 |
| `Mirror` | リアルタイム反射面 |
| `VideoScreen` | 同期された動画再生 |

### フック

| フック | 説明 |
|-------|------|
| `useInstanceState()` | ユーザー間で状態を同期 |

詳細は [Components](/world-components/components/) を参照してください。

## リポジトリ

- [GitHub: xrift-world-components](https://github.com/WebXR-JP/xrift-world-components)
