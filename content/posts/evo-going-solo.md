---
slug: evo-going-solo
category: devlog
date: 2026-04-01
published: true
title:
  tr: "Evo #1: Solo Yola Çıkmak"
  en: "Evo #1: Going Solo"
excerpt:
  tr: "Herkes solo Metroidvania yapmanın kötü bir fikir olduğunu söyler. Muhtemelen haklılar. Yine de yapıyorum."
  en: "Everyone will tell you making a Metroidvania solo is a bad idea. They're probably right. I'm doing it anyway."
body_en: |
    Everyone will tell you making a Metroidvania solo is a bad idea. They're probably right. I'm doing it anyway.

    Evo started in April 2025 as an experiment — could I build a game that felt as interconnected and responsive as the classics (Hollow Knight, Ori, Symphony of the Night) without a team? A year in, I have a partial answer: yes, but it takes a very specific approach.

    ## The Scope Problem

    Metroidvanias are defined by their interconnected world, ability gating, and exploration. Every corridor you add implies a reason to return to it. The scope can spiral infinitely. My solution: design in "rings." The first ring is one self-contained zone with 3 abilities and a boss. Get that working perfectly before expanding outward.

    ## Tech Stack

    I'm building in Godot 4.3. The choice was easy — it's free, open source, the scene system maps beautifully to my FSM architecture, and GDScript is fast enough for iteration. I write shaders in GLSL directly, and I use Aseprite for all art.

    ## What's Working

    The FSM system is solid. Player states (Idle, Run, Jump, WallSlide, Dash, Attack) transition cleanly with no boolean soup. The camera feel is close — I'm using a spring-damper system for follow with a small lookahead based on velocity direction.

    ## What Isn't

    Enemy AI is placeholder. The first boss exists as a hitbox with a health bar. The first ability (wall jump) works but needs more coyote time tuning. Ring 1 is about 40% playable.

    Next update when Ring 1 is beatable start to finish.
body_tr: |
    Herkes solo Metroidvania yapmanın kötü bir fikir olduğunu söyler. Muhtemelen haklılar. Yine de yapıyorum.

    Evo, Nisan 2025'te bir deney olarak başladı — takım olmadan klasikler (Hollow Knight, Ori, Symphony of the Night) kadar bağlantılı ve duyarlı bir oyun yapabilir miyim? Bir yıl sonra kısmi bir cevabım var: evet, ama çok özgül bir yaklaşım gerektiriyor.

    ## Kapsam Sorunu

    Metroidvania'lar birbirine bağlı dünya, yetenek kapıları ve keşifle tanımlanır. Eklediğin her koridor, oraya geri dönmek için bir neden ima eder. Kapsam sonsuzca sarmal olabilir. Çözümüm: "halkalar" halinde tasarlamak. İlk halka, 3 yetenekli ve patronlu, kendi içinde tam bir bölge. Dışarı genişlemeden önce mükemmel çalıştır.

    ## Teknoloji Yığını

    Godot 4.3 ile yapıyorum. Seçim kolaydı — ücretsiz, açık kaynak, sahne sistemi FSM mimarime güzel uyuyor ve GDScript iterasyon için yeterince hızlı. Shader'ları doğrudan GLSL ile yazıyorum, tüm sanat için Aseprite kullanıyorum.

    ## Çalışan Şeyler

    FSM sistemi sağlam. Oyuncu durumları (Boşta, Koş, Zıpla, DuvarKay, Dash, Saldır) boolean çorbası olmadan temiz geçiş yapıyor. Kamera hissi yakın — hıza dayalı küçük bir lookahead ile takip için yay-damper sistemi kullanıyorum.

    ## Çalışmayan Şeyler

    Düşman yapay zekası geçici. İlk patron, sağlık çubuğu olan bir hitbox olarak var. İlk yetenek (duvar zıplaması) çalışıyor ama daha fazla coyote time ayarı gerekiyor. Halka 1 yaklaşık %40 oynanabilir.

    Halka 1 baştan sona oynanabilir olduğunda sonraki güncelleme.
---
