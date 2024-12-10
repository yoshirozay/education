# Scroll Transition

## Description
A custom scroll transition effect for SwiftUI views

## Example Usage
```swift
ScrollView {
    LazyStack(spacing: -20) {
        ForEach(0..<20) { index in
            CardView(index: index)
                .scrollTransition { effect, phase in
                    effect
                }
        }
    }
}
