import SwiftUI

@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
                .environment(\.managedObjectContext, Persistence.shared.container.viewContext)
        }
    }
}

import CoreData

class Persistence {
    static let shared = Persistence()
    
    let container: NSPersistentContainer
    
    init(inMemory: Bool = false) {
        let clabeEntity = NSEntityDescription()
        clabeEntity.name = "Clabe"
        clabeEntity.managedObjectClassName = "Clabe"
        
        let clabeAttribute = NSAttributeDescription()
        clabeAttribute.name = "clabe"
        clabeAttribute.type = .string
        clabeEntity.properties.append(clabeAttribute)
        
        let nameAttribute = NSAttributeDescription()
        nameAttribute.name = "name"
        nameAttribute.type = .string
        clabeEntity.properties.append(nameAttribute)
        
        let bankAttribute = NSAttributeDescription()
        bankAttribute.name = "bank"
        bankAttribute.type = .string
        clabeEntity.properties.append(bankAttribute)
        
        let photoAttribute = NSAttributeDescription()
        photoAttribute.name = "photo"
        photoAttribute.type = .binaryData
        clabeEntity.properties.append(photoAttribute)
        
        let model = NSManagedObjectModel()
        model.entities = [clabeEntity]
        
        let container = NSPersistentContainer(name: "ClabeModel", managedObjectModel: model)
        
        if inMemory {
            container.persistentStoreDescriptions.first!.url = URL(fileURLWithPath: "/dev/null")
        }
        
        container.loadPersistentStores { description, error in
            if let error = error {
                print("Failed with: \(error.localizedDescription)")
            }
        }
        
        container.viewContext.mergePolicy = NSMergeByPropertyObjectTrumpMergePolicy
        container.viewContext.automaticallyMergesChangesFromParent = true
        
        self.container = container
    }
}
