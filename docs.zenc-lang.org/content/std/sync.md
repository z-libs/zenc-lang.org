+++
title = "std/sync"
+++

# std/sync

The `std/sync` module provides synchronization primitives for multithreading, including mutexes, condition variables, reader-writer locks, one-time initialization, semaphores, and barriers.

## Usage

```zc
import "std/sync.zc"

fn main() {
    let m = Mutex::new();
    m.lock();
    // Critical section
    m.unlock();
}
```

## Struct Definitions

### `Mutex`
A mutual exclusion lock. Implements `Drop` for automatic resource cleanup.

### `CondVar`
A condition variable for thread signaling. Implements `Drop`.

### `RwLock`
A reader-writer lock. Implements `Drop`.

### `Once`
A primitive for one-time initialization. Implements `Drop`.

### `Semaphore`
A counting semaphore. Implements `Drop`.

### `Barrier`
A synchronization barrier. Implements `Drop`.

## Methods

### `Mutex` Methods
| Method | Signature | Description |
| :--- | :--- | :--- |
| **new** | `Mutex::new() -> Mutex` | Creates a new mutex. |
| **lock** | `lock(self)` | Acquires the lock (blocking). |
| **try_lock** | `try_lock(self) -> bool` | Attempts to acquire the lock without blocking. Returns `true` if successful. |
| **unlock** | `unlock(self)` | Releases the lock. |
| **free** | `free(self)` | Manually destroys the mutex. |

### `CondVar` Methods
| Method | Signature | Description |
| :--- | :--- | :--- |
| **new** | `CondVar::new() -> CondVar` | Creates a new condition variable. |
| **wait** | `wait(self, mutex: Mutex*)` | Waits on the condition variable, releasing the mutex. |
| **signal** | `signal(self)` | Signals one waiting thread. |
| **broadcast**| `broadcast(self)` | Signals all waiting threads. |
| **free** | `free(self)` | Manually destroys the condition variable. |

### `RwLock` Methods
| Method | Signature | Description |
| :--- | :--- | :--- |
| **new** | `RwLock::new() -> RwLock` | Creates a new reader-writer lock. |
| **rdlock** | `rdlock(self)` | Acquires the read lock (blocking). |
| **try_rdlock**| `try_rdlock(self) -> bool` | Attempts to acquire the read lock without blocking. |
| **wrlock** | `wrlock(self)` | Acquires the write lock (blocking). |
| **try_wrlock**| `try_wrlock(self) -> bool` | Attempts to acquire the write lock without blocking. |
| **unlock** | `unlock(self)` | Releases the lock. |
| **free** | `free(self)` | Manually destroys the lock. |

### `Once` Methods
| Method | Signature | Description |
| :--- | :--- | :--- |
| **new** | `Once::new() -> Once` | Creates a new one-time initialization handle. |
| **call** | `call(self, func: fn())` | Executes `func` exactly once across all threads. |
| **free** | `free(self)` | Manually destroys the handle. |

### `Semaphore` Methods
| Method | Signature | Description |
| :--- | :--- | :--- |
| **new** | `Semaphore::new(value: int) -> Semaphore` | Creates a new semaphore with initial `value`. |
| **wait** | `wait(self)` | Decrements the semaphore (blocking if 0). |
| **try_wait** | `try_wait(self) -> bool` | Attempts to decrement without blocking. Returns `true` if successful. |
| **post** | `post(self)` | Increments the semaphore. |
| **value** | `value(self) -> int` | Returns the current semaphore value. |
| **free** | `free(self)` | Manually destroys the semaphore. |

### `Barrier` Methods
| Method | Signature | Description |
| :--- | :--- | :--- |
| **new** | `Barrier::new(count: int) -> Barrier` | Creates a new barrier for `count` threads. |
| **wait**| `wait(self) -> bool` | Waits at the barrier. Returns `true` if this thread was the serial thread leader. |
| **free** | `free(self)` | Manually destroys the barrier. |
