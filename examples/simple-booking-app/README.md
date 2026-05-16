# Example: Simple Booking App

This is a small example showing how the template should be used. It is not a complete app.

## Raw Design Input

A local studio wants a simple booking MVP.

Customers should be able to choose a service, pick a time slot, enter contact information, and submit a booking request. The studio owner should be able to review requests and mark them as accepted or rejected.

The MVP should not take online payments yet. It should not expose private customer phone numbers publicly. Customers should receive clear feedback after submitting a request. The owner should be able to see enough information to follow up manually.

## Extracted Product Truth

- This is a booking request tool, not an instant paid reservation system.
- The MVP proves request intake and owner review.
- Payment, automatic calendar sync, and SMS reminders are future work.

## Core Rules

- A booking request is not confirmed until the owner accepts it.
- Customer contact information is private.
- Disabled future features must not appear as working UI.
- Local demo data must not be treated as production data.

## PM Questions

1. Can customers cancel a request in MVP?
2. Can two customers request the same time slot before owner review?
3. Does the owner need email notifications in MVP, or is dashboard review enough?
4. What information is required: name, phone, email, notes?

## Capability Loop Example

| Capability | UI | API | Data | Permission | Error | Verification |
|---|---|---|---|---|---|---|
| Submit booking request | Service/time/contact form | create request | booking_requests | public create only | invalid slot/contact | local smoke + integration |
| Owner review | dashboard list/actions | accept/reject request | status transition | owner only | stale request | integration + protected route smoke |

## Defense Notes

- Rate limit public submissions.
- Do not expose customer contact data in public URLs.
- Owner actions should be auditable.
- Duplicate submissions should be handled gracefully.
