# Scroll Transition

## Description
A custom scroll transition effect for SwiftUI views

## Example Usage
```swift

struct ContentView: View {
    var body: some View {
        ScrollView {
            LazyVStack(spacing: -20) {
                ForEach(0..<20) { index in
                    CardView(index: index)
                        .scrollTransition { effect, phase in
                            effect
                                .opacity(phase.isIdentity ? 1 : 0)
                                .scaleEffect(phase.isIdentity ? 1 : 0.3)
                                .blur(radius: phase.isIdentity ? 0 : 10)
                                .offset(x: offset(for: phase))
                                
                        }
                }
            }
            .padding()
        }
    }
    nonisolated func offset(for phase: ScrollTransitionPhase) -> Double {
        switch phase {
        case .topLeading:
            -200
        case .identity:
            0
        case .bottomTrailing:
            0
        }
    }
}

struct CardView: View {
    let index: Int
    
    var body: some View {
        RoundedRectangle(cornerRadius: 12)
            .fill(Color.orange.opacity(1))
            .frame(width: 250, height: 250)
            .overlay(Text("Card \(index)"))
            .shadow(color: .black.opacity(0.25), radius: 10, y: 6)
    }
}

#Preview {
    ContentView()
}

