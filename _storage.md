# Cities Skylines 2 ModAPI Specification - Storage API

## Overview
This document specifies the Storage API for Cities Skylines 2, designed to mirror the style of official .NET libraries. It provides a standardized way for modders to interact with various storage types within the game.

## Enumerations

### StorageKind
Enumerates the types of storage available in the game.

- `Local`: Local storage, specific to the user's local machine.
- `Session`: Session storage, lasting for the duration of the game session.
- `SaveGame`: Storage tied to a specific save game.
- `Config`: Configuration storage for mod settings and preferences.

## Interfaces

### IStorageProvider
Interface for handling storage operations, following .NET best practices.

#### Methods

##### T Read<T>(StorageKind kind, string key)
Reads and retrieves an item of a specified type from storage.

- `T`: The type of the item to retrieve.
- `kind`: The kind of storage to access (Local, Session, SaveGame, Config).
- `key`: The key identifying the item in storage.

Returns an item of type `T` associated with the specified key.

##### void Write<T>(StorageKind kind, string key, T value)
Writes and stores an item in the specified storage kind.

- `kind`: The kind of storage to use (Local, Session, SaveGame, Config).
- `key`: The key under which to store the item.
- `value`: The item of type `T` to store.

## Example Usage

```csharp
// Example usage of IStorageProvider
public class ModExample
{
    private readonly IStorageProvider _storageProvider;

    public ModExample(IStorageProvider storageProvider)
    {
        _storageProvider = storageProvider;
    }

    public void DemonstrateStorage()
    {
        // Read an item from local storage
        var item = _storageProvider.Read<MyDataType>(StorageKind.Local, "myDataKey");

        // Write an item to configuration storage
        _storageProvider.Write(StorageKind.Config, "configKey", item);
    }
}
