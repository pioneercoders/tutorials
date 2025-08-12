#### 1. What is the difference between ngOnChanges() and ngDoCheck()? When would you use each?

ngOnChanges()

- Triggered when an @Input() property changes (value by reference for objects/arrays).

- Runs before ngOnInit().

ngDoCheck()

- Runs on every change detection cycle, regardless of whether the inputs have changed.

- Used for custom change detection (e.g., deep checking arrays/objects).

Use Case:

ngOnChanges() for reacting to direct input changes.

ngDoCheck() when Angular’s default change detection isn’t enough.

#### 2.How does Angular’s change detection mechanism work? How can you optimize it?

- Angular uses Zone.js to patch async APIs and trigger change detection in a tree of components.

- Default strategy: ChangeDetectionStrategy.Default — checks all components on every change detection cycle.

Optimization:

- Use ChangeDetectionStrategy.OnPush to only run detection when @Input() reference changes.

- Use trackBy with *ngFor to prevent unnecessary DOM re-rendering.

- Manually trigger detection with ChangeDetectorRef.markForCheck() or detectChanges().

#### 3.What’s the difference between BehaviorSubject, Subject, and ReplaySubject in Angular services?

| Type                | Initial Value? | Stores Last Value? | Emits Past Values?                 |
| ------------------- | -------------- | ------------------ | ---------------------------------- |
| **Subject**         | No             | No                 | No                                 |
| **BehaviorSubject** | Yes            | Yes                | Last value only                    |
| **ReplaySubject**   | No             | Yes                | Multiple past values (buffer size) |

Use Case in Angular:

- Subject for event streams.

- BehaviorSubject for state management (last value always available).

- ReplaySubject for caching and replaying history.

#### 4.Explain the difference between forRoot() and forChild() in Angular modules.

forRoot()

Used in the root module to provide singleton services across the app.

Example: RouterModule.forRoot(routes)

forChild()

Used in feature modules to register routes without creating new service instances.

Example: RouterModule.forChild(routes)



#### 5.How would you handle memory leaks in Angular applications?
- Causes:

  - Unsubscribed Observables.

  - Detached DOM nodes with event listeners.

  - Long-lived services holding stale references.

- Prevention:

  - Use async pipe for template bindings.

  - Use takeUntil() or Subscription.unsubscribe() in ngOnDestroy().

  - Avoid global event listeners unless removed.
 
#### 6.What’s the difference between ActivatedRoute snapshot and observable in Angular routing?
- Snapshot:

  - this.route.snapshot.paramMap.get('id') — gets the value once.

- Observable:

  - this.route.paramMap.subscribe(...) — reacts to parameter changes (e.g., when navigating within the same component).
