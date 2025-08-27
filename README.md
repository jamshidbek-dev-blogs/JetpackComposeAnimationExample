# Jetpack Compose Animation Example ✨

[![Android](https://img.shields.io/badge/Platform-Android-green?logo=android)](https://www.android.com/)
[![Kotlin](https://img.shields.io/badge/Language-Kotlin-blue?logo=kotlin)](https://kotlinlang.org/)
[![Jetpack Compose](https://img.shields.io/badge/Jetpack-Compose-4285F4?logo=jetpackcompose&logoColor=white)](https://developer.android.com/jetpack/compose)

Stop Writing Clunky UIs. Jetpack Compose Animations Are Easier Than You Think.

This project demonstrates how to build smooth, declarative animations in **Jetpack Compose** with just a few lines of code. No more `AnimatorSet`, no more boilerplate — just state-driven UI updates that *feel alive*.

---
## 🎥 Demo

<video src="media/demo.mp4" controls width="500"></video>

*Click the play button above to see the card expand with smooth animations.*


## 📝 Blog Post

This repo accompanies the article:  
**[Stop Writing Clunky UIs. Jetpack Compose Animations Are Easier Than You Think.](https://jamshidbekboynazarov.medium.com/stop-writing-clunky-uis-jetpack-compose-animations-are-easier-than-you-think-ead9dbfba913)** (Medium, August 2025) :contentReference[oaicite:0]{index=0}

---

## 🚀 Why Animations Matter

In the old days, even a simple fade-in required `AnimatorSet`, `ViewPropertyAnimator`, or `XML transitions`. It was messy, hard to manage, and often skipped entirely.

But subtle animations are what make an app feel polished and intuitive. With Compose, animations are **part of the declarative UI** — no excuses anymore.

---

## 🛠 Core Idea: Animate State Changes

In Compose, the UI is a function of **state**. When state changes, the UI recomposes.  
Animations are simply the *transition* between the “before” and “after” of that state.

- **`animate*AsState`** → smoothly animates simple values like color, size, alpha, padding.
- **`AnimatedVisibility`** → handles content appearing/disappearing with enter/exit transitions.

---

## 📦 Example: Expandable Card

```kotlin
@Composable
fun ExpandableCard() {
    var expanded by remember { mutableStateOf(false) }

    // Animate background color based on state
    val backgroundColor by animateColorAsState(
        targetValue = if (expanded) MaterialTheme.colorScheme.primaryContainer
                      else MaterialTheme.colorScheme.surfaceVariant,
        label = "backgroundColorAnimation"
    )

    Card(
        modifier = Modifier
            .fillMaxWidth()
            .padding(16.dp)
            .clickable { expanded = !expanded },
        colors = CardDefaults.cardColors(containerColor = backgroundColor)
    ) {
        Column(modifier = Modifier.padding(16.dp)) {
            Text(text = "Tap to Expand", style = MaterialTheme.typography.titleMedium)

            // Animate presence with fade + slide
            AnimatedVisibility(visible = expanded) {
                Text(
                    text = "Here are the extra details! They fade and slide in smoothly, making the UI feel polished.",
                    modifier = Modifier.padding(top = 8.dp)
                )
            }
        }
    }
}
