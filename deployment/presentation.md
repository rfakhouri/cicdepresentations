# Deployment

------

Pretty much just copying some files to a server.

------

Thank You have a nice day.

---

## Recreate

------

Probably what 99% of you are doing right now.

------

**Pros:**

Easy to setup.
Application state entirely renewed.

**Cons:**

High impact on the user, expect downtime that depends on both shutdown and boot duration of the application.

---

Blue/Green

------

**Pros:**

Instant rollout/rollback.
Avoid versioning issue, the entire application state is changed in one go.

**Cons:**

Expensive as it requires double the resources.
Proper test of the entire platform should be done before releasing to production.
Handling stateful applications can be hard.

---

Canary

------


**Pros:**

Version released for a subset of users.
Convenient for error rate and performance monitoring.
Fast rollback.

**Con:**

Slow rollout.

---

Ramped

------

**Pros:**

Easy to set up.
Version is slowly released across instances.
Convenient for stateful applications that can handle rebalancing of the data.

**Cons:**

Rollout/rollback can take time.
Supporting multiple APIs is hard.
No control over traffic.

---

Shadow

------

**Pros:**

Performance testing of the application with production traffic.
No impact on the user.
No rollout until the stability and performance of the application meet the requirements.

**Cons:**

Expensive as it requires double the resources.
Not a true user test and can be misleading.
Complex to setup.
Requires mocking service for certain cases.

---

Special Mention

------

A/B Testing</section>

------

**Pros:**

Several versions run in parallel.
Full control over the traffic distribution.

**Cons:**

Requires intelligent load balancer.
Hard to troubleshoot errors for a given session, distributed tracing becomes mandatory.

---

References

- https://thenewstack.io/deployment-strategies/