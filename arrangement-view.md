# Arrangement View

## Example 

https://github.com/user-attachments/assets/3a12465d-0f74-440f-8309-e156b217f4e0

Try? it out 

```swift
struct ArrangementCard: View {
    let imageName: String
    let text: String

    var body: some View {
        ZStack {
            Image(imageName)
                .resizable()
                .aspectRatio(contentMode: .fill)
            Text(text)
                .background(.black)
        }
    }
}

struct ContentView: View {
    var body: some View {
        if #available(iOS 27.1, *) {
            NavigationStack {
                ArrangementView {
                    ArrangementCard(
                        imageName: "miles-at-0",
                        text: "Miles at birth"
                    )
                } secondary: {
                    ArrangementCard(
                        imageName: "miles-at-14",
                        text: "14 years later"
                    )
                }
                // Handles both `.vertical` and `.horizontal` axes
                // .arrangementViewStyle(.split)

                // We can restrict which axes is visible, in this case only when split horizontal
                .arrangementViewStyle(.split.axes(.horizontal))

                .foregroundStyle(.white)
                .font(.largeTitle)
                .ignoresSafeArea()
            }
        } else {
            ContentUnavailableView {
                Label("OS Not Available", systemImage: "exclamationmark.triangle.fill")
            } description: {
                Text("You need to be running iOS 27.1 or higher")
            }
        }
    }
}

#Preview {
    ContentView()
}
```
