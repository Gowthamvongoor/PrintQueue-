# PrintQueue — Smart Campus Printing Queue System

A standard-JDK, console-based campus print-centre simulation. It uses FIFO `Queue`, synchronized reservations, background `Runnable` print jobs, SHA-256 password hashes, and Base64-safe CSV fields in `data/`.

## Run

```powershell
javac -d out src\PrintQueue.java
java -cp out PrintQueue
```

For fast, non-animated smoke tests:

```powershell
java -Dprintqueue.noAnimation=true -Dprintqueue.noColor=true -cp out PrintQueue
```

## Demo administrator

- Username: `admin`
- Password: `PrintQueue@2026`

Student passwords are never stored in plaintext. Data files are rewritten atomically at the application-service level (`save` is synchronized); this is suitable for a classroom demo, not concurrent multi-process access.

## Features

- Student registration, login, private orders, tracking, cancellation and collection
- FIFO pending queue with live visual monitor and real queue positions
- Administrator queue processing, printer monitoring/status changes, reports and order history
- Valid status transitions: pending → in progress → ready → collected; pending → cancelled
- Two persisted sample printers and persisted job completion counts
- Controlled threaded print simulation (the administrator waits on one worker so terminal input and animations do not collide)
