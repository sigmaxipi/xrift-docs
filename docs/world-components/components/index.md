---
sidebar_position: 1
---

# API リファレンス

xrift-world-components で提供されるコンポーネントとフックの一覧です。

## コンポーネント

### Interactable

クリック/インタラクト可能なオブジェクトを作成します。

```tsx
import { Interactable } from '@xrift/world-components';

<Interactable id="my-button" onInteract={() => console.log('clicked!')}>
  <mesh>
    <boxGeometry args={[1, 1, 1]} />
    <meshStandardMaterial color="hotpink" />
  </mesh>
</Interactable>
```

#### Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `id` | `string` | - | 一意の識別子（必須） |
| `onInteract` | `() => void` | - | インタラクト時のコールバック |
| `children` | `ReactNode` | - | インタラクト対象のオブジェクト |

---

### Mirror

リアルタイム反射面を作成します。

```tsx
import { Mirror } from '@xrift/world-components';

<Mirror position={[0, 1, -5]} />
```

---

### VideoScreen

同期された動画再生を行うスクリーンを作成します。

```tsx
import { VideoScreen } from '@xrift/world-components';

<VideoScreen src="/videos/intro.mp4" position={[0, 2, -3]} />
```

---

## フック

### useInstanceState

ワールド内の全ユーザー間で状態を同期します。React の `useState` と同じインターフェースです。

```tsx
import { useInstanceState } from '@xrift/world-components';

function Counter() {
  const [count, setCount] = useInstanceState('counter', 0);

  return (
    <mesh onClick={() => setCount(count + 1)}>
      {/* count は全ユーザーで同期される */}
    </mesh>
  );
}
```

#### 引数

| 引数 | Type | Description |
|-----|------|-------------|
| `key` | `string` | 状態の一意な識別子 |
| `initialValue` | `T` | 初期値 |

#### 戻り値

`[value: T, setValue: (newValue: T) => void]` - useState と同じ形式
