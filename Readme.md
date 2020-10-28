# The Next Car
Aplikasi ini merupakan sebuah program yang menggunakan konsep MVC untuk diterapkan pada sebuah mobil berbasis tekhnologi modern, dengan tujuan mengutamakan keselamatan.

## Scope & Functionalities
-  User dapat menekan tombol STARTED, CLOSE/CLOSED, LOCK/LOCKED, OFF/ON 
-  User hanya dapat menekan tombol STARTED, apabila semua perintah telah terpenuhi

## How Does it Works?
Logika pada `DoorController.cs` di awali dengan mendeklarasikan  
```csharp
class DoorController
    {
        private Door door;
        private OnDoorChanged callbackOnDoorChanged;

        public DoorController(OnDoorChanged callbackOnDoorChanged)
        {
            this.callbackOnDoorChanged = callbackOnDoorChanged;
            this.door = new Door();
        }

        public void close()
        {
            this.door.close();
            this.callbackOnDoorChanged.onDoorOpenStateChanged("CLOSED", "door closed");
        }
        public void open()
        {
            this.door.open();
            this.callbackOnDoorChanged.onDoorOpenStateChanged("OPENED", "door opened");
        }
        public void activateLock()
        {
            this.door.activatelock();
            this.callbackOnDoorChanged.onDoorOpenStateChanged("LOCKED", "door locked");
        }
        public void unlock()
        {
            this.door.unlock();
            this.callbackOnDoorChanged.onDoorOpenStateChanged("UNLOCK", "door unlocked");
        }
        public bool isClose()
        {
            return this.door.isClosed();
        }
        public bool isLocked()
        {
            return this.door.isLocked();
        }
    }
```

Pada class `Door.cs` ini, berfungsi untuk mendeklarasikan class `DoorController.cs` dengan source code seperti berikut
```csharp
class Door
    {
        private bool locked;
        private bool closed;

        public void close()
        {
            this.closed = true;
        }

        public void open()
        {
            this.closed = false;
        }

        public void activatelock()
        {
            this.locked = true;
        }

        public void unlock()
        {
            this.locked = false;
        }

        public bool isLocked()
        {
            return this.locked;
        }

        public bool isClosed()
        {
            return this.closed;
        }
    }
```