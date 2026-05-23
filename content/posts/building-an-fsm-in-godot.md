---
slug: building-an-fsm-in-godot
category: tutorial
date: 2026-05-01
published: true
title:
  tr: "Godot'ta FSM Tasarlamak"
  en: "Building an FSM in Godot"
excerpt:
  tr: "Karakter durumlarını temiz bir şekilde yönetmek için Sonlu Durum Makinesi nasıl kurulur — spagetti koddan ve iç içe if-else zincirlerinden kaçınarak."
  en: "How I architect Finite State Machines to handle player states cleanly — avoiding spaghetti code and nested if-else chains."
body_en: |
    When I started working on Evo, one of the first architectural decisions I had to make was how to handle character states. Should the player be able to dash while wall-sliding? Can enemies attack while being knocked back? If you don't have a clear system for this, you end up with a massive pile of boolean flags and nested `if` statements.

    The answer I landed on: a clean Finite State Machine (FSM). Here's how I built it in Godot.

    ## What's a Finite State Machine?

    An FSM is a model where your character can be in exactly one *state* at a time — Idle, Running, Jumping, Dashing, etc. — and transitions between states are explicitly defined. It forces you to think about what's actually possible.

    ## The Base State Class

    ```gdscript
    class_name State extends Node

    var character: CharacterBody2D

    func enter() -> void: pass
    func exit() -> void: pass
    func update(delta: float) -> void: pass
    func physics_update(delta: float) -> void: pass
    func get_transition() -> String: return ""
    ```

    Every state inherits from this. `get_transition()` returns the key of the next state, or an empty string if no transition should happen.

    ## The State Machine

    ```gdscript
    class_name StateMachine extends Node

    @export var initial_state: State
    var current_state: State

    func _ready() -> void:
        current_state = initial_state
        current_state.enter()

    func _process(delta: float) -> void:
        current_state.update(delta)
        var next = current_state.get_transition()
        if next != "":
            transition_to(next)

    func _physics_process(delta: float) -> void:
        current_state.physics_update(delta)

    func transition_to(state_key: String) -> void:
        current_state.exit()
        current_state = get_node(state_key)
        current_state.enter()
    ```

    ## Why This Works

    The key insight: each state is completely isolated. The `Dash` state doesn't need to know anything about `WallSlide`. If `Dash` ends and the player is touching a wall, `get_transition()` returns `"WallSlide"`. That's it.

    No more `if is_dashing and is_on_wall and not is_attacking`. Just clean, readable state logic.
body_tr: |
    Evo üzerinde çalışmaya başladığımda ilk mimari kararlardan biri karakter durumlarını nasıl yöneteceğimdi. Oyuncu duvar kayarken dash yapabilmeli mi? Düşmanlar geri itilirken saldırabilmeli mi? Net bir sistem yoksa sonunda devasa bir boolean yığını ve iç içe `if` ifadeleri ortaya çıkıyor.

    Vardığım cevap: temiz bir Sonlu Durum Makinesi (FSM). Godot'ta nasıl oluşturduğumu anlatıyorum.

    ## Sonlu Durum Makinesi Nedir?

    FSM, karakterin aynı anda tam olarak bir *durumda* olabileceği bir modeldir — Boşta, Koşuyor, Zıplıyor, Dash vb. — ve durumlar arası geçişler açıkça tanımlanır. Gerçekte nelerin mümkün olduğunu düşünmeye zorlar.

    ## Temel State Sınıfı

    ```gdscript
    class_name State extends Node

    var character: CharacterBody2D

    func enter() -> void: pass
    func exit() -> void: pass
    func update(delta: float) -> void: pass
    func physics_update(delta: float) -> void: pass
    func get_transition() -> String: return ""
    ```

    Her durum bundan miras alır. `get_transition()` bir sonraki durumun anahtarını döndürür; geçiş olmaması gerekiyorsa boş string döner.

    ## State Machine

    ```gdscript
    class_name StateMachine extends Node

    @export var initial_state: State
    var current_state: State

    func _ready() -> void:
        current_state = initial_state
        current_state.enter()

    func _process(delta: float) -> void:
        current_state.update(delta)
        var next = current_state.get_transition()
        if next != "":
            transition_to(next)

    func _physics_process(delta: float) -> void:
        current_state.physics_update(delta)

    func transition_to(state_key: String) -> void:
        current_state.exit()
        current_state = get_node(state_key)
        current_state.enter()
    ```

    ## Neden Çalışıyor?

    Kilit nokta: her durum tamamen izole. `Dash` durumunun `WallSlide` hakkında hiçbir şey bilmesi gerekmiyor. `Dash` bittiğinde oyuncu duvara değiyorsa `get_transition()` `"WallSlide"` döndürür. Hepsi bu.

    Artık `if is_dashing and is_on_wall and not is_attacking` yok. Sadece temiz, okunabilir durum mantığı.
---
