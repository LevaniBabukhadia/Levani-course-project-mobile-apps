import SwiftUI

// MARK: - Car Model
struct Car: Identifiable {
    let id = UUID()
    let brand: String
    let year: Int
    let price: Double
    let imageName: String // Name of the image in the Assets catalog
}

// MARK: - Horizontal Car List View
struct HorizontalCarListView: View {
    // Sample data
    let cars = [
        Car(brand: "Toyota", year: 2020, price: 25000.0, imageName: "toyota"),
        Car(brand: "BMW", year: 2023, price: 45000.0, imageName: "bmw"),
        Car(brand: "Audi", year: 2022, price: 40000.0, imageName: "audi")
    ]
    
    var body: some View {
        ScrollView(.horizontal, showsIndicators: false) {
            HStack(spacing: 16) {
                ForEach(cars) { car in
                    CarCardView(car: car)
                }
            }
            .padding()
        }
    }
}

// MARK: - Car Card View
struct CarCardView: View {
    let car: Car
    
    var body: some View {
        VStack {
            Image(car.imageName)
                .resizable()
                .scaledToFit()
                .frame(width: 150, height: 100)
                .cornerRadius(8)
            
            Text(car.brand)
                .font(.headline)
            
            Text("Year: \(car.year)")
                .font(.subheadline)
                .foregroundColor(.gray)
            
            Text("$\(car.price, specifier: "%.2f")")
                .font(.subheadline)
                .foregroundColor(.blue)
        }
        .frame(width: 160)
        .background(Color.white)
        .cornerRadius(12)
        .shadow(radius: 4)
    }
}

// MARK: - Main Content View
struct ContentView: View {
    var body: some View {
        HorizontalCarListView()
    }
}

// MARK: - Main App Entry Point
@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
