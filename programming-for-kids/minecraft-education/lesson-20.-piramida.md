# Урок 20. Піраміда

### Квадрат

![](<../../.gitbook/assets/Minecraft Education Edition (6).jpg>)

![](<../../.gitbook/assets/Minecraft Education Edition\_code.jpg>)

#### Код:

```
player.onChat("s", function () {
    agent.setItem(EMERALD_BLOCK, 1, 1)
    agent.setSlot(1)
    agent.move(UP, 1)
    for (let index = 0; index < 4; index++) {
        for (let index = 0; index < 5; index++) {
            agent.place(DOWN)
            agent.move(FORWARD, 1)
        }
        agent.turn(LEFT_TURN)
    }
    agent.move(FORWARD, 1)
    agent.move(LEFT, 1)
})
```

### Основа

![](../../.gitbook/assets/base.jpg)

![](../../.gitbook/assets/base\_code.jpg)

#### Код:

```
player.onChat("base", function (Ширина) {
    agent.setItem(EMERALD_BLOCK, 1, 1)
    agent.setSlot(1)
    agent.move(UP, 1)
    n = Ширина / 2
    for (let index = 0; index < n; index++) {
        for (let index = 0; index < 4; index++) {
            for (let index = 0; index < Ширина; index++) {
                agent.place(DOWN)
                agent.move(FORWARD, 1)
            }
            agent.turn(LEFT_TURN)
        }
        agent.move(FORWARD, 1)
        agent.move(LEFT, 1)
        Ширина += -2
    }
    agent.place(DOWN)
})
```

## Пирамида

![](../../.gitbook/assets/pir\_.jpg)

![](../../.gitbook/assets/pir.jpg)

![](../../.gitbook/assets/pir\_2.jpg)

![](../../.gitbook/assets/pir\_light.jpg)

#### Код:

```
player.onChat("pir", function () {
    agent.setItem(EMERALD_BLOCK, 1, 1)
    agent.setSlot(1)
    agent.move(UP, 1)
    n = 2
    k = n
    for (let index = 0; index < k; index++) {
        Ширина = n * 2
        for (let index = 0; index < n; index++) {
            for (let index = 0; index < 4; index++) {
                for (let index = 0; index < Ширина; index++) {
                    agent.place(DOWN)
                    agent.move(FORWARD, 1)
                }
                agent.turn(LEFT_TURN)
            }
            agent.move(FORWARD, 1)
            agent.move(LEFT, 1)
            Ширина += -2
        }
        agent.place(DOWN)
        n += -1
        agent.move(BACK, n)
        agent.move(RIGHT, n)
        agent.move(UP, 1)
    }
    player.runChatCommand("light")
})

player.onChat("light", function () {
    agent.setItem(BEACON, 1, 1)
    agent.place(DOWN)
})
```
