---
slug: building-an-fsm-in-godot
category: tutorial
date: 2026-05-01
published: true
title:
  tr: "Godot'ta FSM Tasarlamak"
  en: "Building an FSM in Godot"
excerpt:
  tr: "ÃÂÃÂÃÂÃÂ§ÃÂ¶iÃÂfdÃÂlfÃÂ¶eÃÂplf deneme"
  en: "How I architect Finite State Machines to handle player states cleanly ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ avoiding spaghetti code and nested if-else chains."
body_en: |
    When I started working on Evo, one of the first architectural decisions I had to make was how to handle character states. Should the player be able to dash while wall-sliding? Can enemies attack while being knocked back? If you don't have a clear system for this, you end up with a massive pile of boolean flags and nested `if` statements.
    
    The answer I landed on: a clean Finite State Machine (FSM). Here's how I built it in Godot.
    
    ## What's a Finite State Machine?
    
    An FSM is a model where your character can be in exactly one *state* at a time ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ Idle, Running, Jumping, Dashing, etc. ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ and transitions between states are explicitly defined. It forces you to think about what's actually possible.
    
    ## The Base State Class
    
    ```
    class_name State extends Nodevar character: CharacterBody2Dfunc enter() -> void: passfunc exit() -> void: passfunc update(delta: float) -> void: passfunc physics_update(delta: float) -> void: passfunc get_transition() -> String: return ""
    ```
    
    Every state inherits from this. `get_transition()` returns the key of the next state, or an empty string if no transition should happen.
    
    ## The State Machine
    
    ```
    class_name StateMachine extends Node@export var initial_state: Statevar current_state: Statefunc _ready() -> void:    current_state = initial_state    current_state.enter()func _process(delta: float) -> void:    current_state.update(delta)    var next = current_state.get_transition()    if next != "":        transition_to(next)func _physics_process(delta: float) -> void:    current_state.physics_update(delta)func transition_to(state_key: String) -> void:    current_state.exit()    current_state = get_node(state_key)    current_state.enter()
    ```
    
    ## Why This Works
    
    The key insight: each state is completely isolated. The `Dash` state doesn't need to know anything about `WallSlide`. If `Dash` ends and the player is touching a wall, `get_transition()` returns `"WallSlide"`. That's it.
    
    No more `if is_dashing and is_on_wall and not is_attacking`. Just clean, readable state logic.
    
    ![eeeeeeeeeeeeeeekkkk](assets/images/frognflies.png)
body_tr: |
    ÃÂÃÂÃÂÃÂ§ÃÂ¶iÃÂfdÃÂlfÃÂ¶eÃÂplf denemedeneme
---
