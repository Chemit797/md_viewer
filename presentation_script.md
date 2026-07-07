# 逐字稿 — Entity Module（2 分钟 · 3 slides）

> 括号内是动作提示，不用说出来。

---

## Slide 1：Inheritance Tree（约 40 秒）

Hello, I am Chen Yuming, and I am responsible for the **entity module**.

The entity module is the core object model of our game.

Let me walk you through how I built the class hierarchy.

We start from the most concrete classes — `Coin`, `EnergyDrink`, and `Magnet`.

When I looked at these three classes, I noticed something.

They all have the same properties — a position, a size, and they all need a spinning animation.

They also all disappear the moment the player touches them.

So instead of writing that logic three times, I extracted it into one abstract class — `Collectible`.

Now, `Player` also needs animation — the running cycle.

So I pulled the animation logic up one more level into `AnimatedObject`.

And finally, every single object in the game world needs coordinates and a size.

So I unified them all under `GameObject`, the abstract base class at the top.

This is our final hierarchy — three levels, each layer adds exactly one responsibility.

---

## Slide 2：Polymorphism（约 40 秒）

（切换到 Slide 2）

Now let me show you why this hierarchy is useful in practice.

`GameWorld` maintains a single list — `List<GameObject>`.

Every frame, the physics loop goes through this list and calls `update()` on each object.

The loop has no idea what it is actually updating.

But at runtime — when `obj` is a `Player`, Java runs `Player`'s own `update()`, which reads the keyboard and applies gravity.

When `obj` is an `Obstacle`, it runs `Obstacle`'s `update()`, which moves it forward along the track.

When `obj` is a `Coin`, it runs the animation timer — just a simple spin.

The same line of code — `obj.update()` — triggers completely different behaviors depending on what `obj` actually is.

The loop itself never changes.

This is **polymorphism**.

---

## Slide 3：LSP（约 40 秒）

（切换到 Slide 3）

This leads us to the **Liskov Substitution Principle**.

The principle states: wherever you use a parent class, you should be able to swap in any subclass — and the program still works correctly.

In our game, `GameWorld` only knows `GameObject`.

It calls `update()`, `isActive()`, and `onCollision()` on each object.

Whether the actual object is a `Player`, an `Obstacle`, or a `Coin` — all of them fulfill this contract correctly.

The loop never crashes. The behavior is always correct.

You can swap any subclass in, and everything still works.

Notice that `GameWorld` never writes `instanceof Player` or `instanceof Coin` to check who it is talking to.

It just calls the method, and trusts the subclass to do the right thing.

That trust is the Liskov Substitution Principle.

Thank you.

---

## 时间参考

| Slide | 内容 | 时长 |
|---|---|---|
| 1 | 继承树构建 | ~40s |
| 2 | 多态 | ~40s |
| 3 | LSP | ~40s |
| **合计** | | **~2 min** |

## 演讲技巧提示
- Slide 1 讲到"发现 Coin、EnergyDrink、Magnet 有共性"时，**稍作停顿**，让听众自己感受到那个"发现问题"的过程
- Slide 2 讲到"The same line of code triggers completely different behaviors"时，**语气加重**，这是整段话最核心的一句
- Slide 3 最后一句 *"That trust is the Liskov Substitution Principle"* 说完之后，**停一秒再说 Thank you**，留给听众反应的时间
