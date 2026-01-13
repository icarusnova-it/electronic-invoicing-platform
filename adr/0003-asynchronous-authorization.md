# ADR-0003: Asynchronous Authorization

## Status

**Accepted** - This architectural decision addresses tax authority reliability.

## Context

Tax authorities have varying response patterns:
- Some respond synchronously (immediate response)
- Most respond asynchronously (callback/webhook)
- Some have unreliable response times
- Some may timeout or fail

We need to decide how to handle authorization responses.

## Decision

**We will design for asynchronous authorization with synchronous fallback and robust retry mechanisms.**

The platform will:

1. **Async-First**: Design for asynchronous authorization
2. **Callback/Webhook**: Support callback/webhook for authorization
3. **Polling Fallback**: Poll for status if callback not received
4. **Retry Logic**: Robust retry mechanisms
5. **Timeout Handling**: Graceful timeout handling

## Consequences

### Positive

✅ **Reliability**: Handles unreliable tax authority responses  
✅ **Scalability**: Async processing scales better  
✅ **User Experience**: Non-blocking operations  
✅ **Resilience**: Handles failures gracefully  

### Negative

❌ **Complexity**: More complex than synchronous  
❌ **State Management**: Need to track pending authorizations  
❌ **Polling Overhead**: Polling adds overhead  

### Mitigation

- Efficient state management
- Smart polling strategies
- Clear state machine
- Good monitoring

## Implementation

### Async Authorization Flow

1. Submit invoice to tax authority
2. Receive submission acknowledgment
3. Wait for authorization callback/webhook
4. Poll for status (fallback)
5. Process authorization response
6. Update invoice status
7. Notify users

### Retry Strategy

**Retry Scenarios:**
- Network failures
- Tax authority timeouts
- Service unavailability
- Rate limiting

**Retry Mechanism:**
- Exponential backoff
- Maximum retry attempts
- Dead letter queue
- Manual intervention

## Related Decisions

- [ADR-0001: Regulator-Agnostic Design](./0001-regulator-agnostic-design.md)
- [Failure and Retry Flow](../diagrams/failure-and-retry-flow.md)

## References

- [Invoice Lifecycle](../docs/invoice-lifecycle.md)
- [Invoice Flow](../diagrams/invoice-flow.md)

---

**Date**: 2026  
**Deciders**: Icarus Nova Architecture Team  
**Status**: Accepted
