# quieo Security Levels Specification

## Overview

quieo implements a comprehensive multi-level security architecture that provides flexible encryption options from no encryption to quantum-secure communication. This specification aligns with the original requirements and provides clear guidance for implementation and usage.

## Security Level Definitions

### Level 0: No Encryption
- **Description**: Standard email transmission without any encryption
- **Use Case**: Public information, non-sensitive communications
- **Implementation**: Direct email transmission via SMTP without encryption
- **Key Management**: No keys required
- **Performance**: Highest (no encryption overhead)
- **Security**: None - suitable only for public information

```typescript
securityLevel: 0
// Result: Standard email sent via SMTP without encryption
```

### Level 1: Standard Encryption (No Quantum Security)
- **Description**: Traditional cryptographic methods without quantum key enhancement
- **Algorithm**: AES-256-GCM with standard key derivation
- **Key Management**: Standard cryptographic key generation using CSPRNG
- **Use Case**: Basic secure communication, legacy system compatibility
- **Performance**: High (standard AES encryption)
- **Security**: Good against classical attacks, vulnerable to quantum attacks

```typescript
securityLevel: 1
// Result: AES-256-GCM encryption with standard key derivation
```

### Level 2: Quantum-aided AES (Recommended Default)
- **Description**: AES-256-GCM encryption using quantum-derived keys as seed
- **Algorithm**: AES-256-GCM with quantum key material via HKDF
- **Key Management**: QKD session provides master key, HKDF derives per-message keys
- **Use Case**: High-security business communications, sensitive data
- **Performance**: High (AES encryption with quantum key derivation)
- **Security**: Excellent - quantum-enhanced classical encryption

```typescript
securityLevel: 2
// Result: AES-256-GCM with quantum-derived keys via HKDF
```

### Level 3: Quantum Secure (One-Time Pad)
- **Description**: True quantum security using One-Time Pad encryption
- **Algorithm**: One-Time Pad (XOR) with quantum key material
- **Key Management**: Direct quantum key consumption (1KB per message)
- **Use Case**: Maximum security for critical communications
- **Performance**: Moderate (limited by key bank consumption)
- **Security**: Perfect secrecy (information-theoretically secure)

```typescript
securityLevel: 3
// Result: One-Time Pad encryption with quantum keys (perfect secrecy)
```

### Level 4: Post-Quantum Cryptography (Future-Proof)
- **Description**: Quantum-resistant cryptography for long-term security
- **Algorithm**: CRYSTALS-Kyber key encapsulation + AES-256-GCM
- **Key Management**: PQC key exchange with hybrid encryption
- **Use Case**: Future-proofing against quantum computer threats
- **Performance**: Moderate (larger key sizes and computations)
- **Security**: Resistant to both classical and quantum attacks

```typescript
securityLevel: 4
// Result: CRYSTALS-Kyber + AES hybrid encryption
```

### Level 5: Legacy Compatibility
- **Description**: Compatibility with existing TLS/PGP systems
- **Algorithm**: TLS 1.3 or PGP encryption
- **Key Management**: Standard PKI or web of trust
- **Use Case**: Interoperability with legacy secure email systems
- **Performance**: Variable (depends on algorithm)
- **Security**: Good (depends on specific implementation)

```typescript
securityLevel: 5
// Result: TLS/PGP encryption for legacy compatibility
```

## Key Bank Management

### Quantum Key Bank
- **Initial Size**: 100 keys of 1KB each per user pair
- **Consumption**: Level 3 (OTP) consumes quantum key material permanently
- **Replenishment**: Automated via QKD sessions when bank drops below threshold
- **Monitoring**: Real-time key bank status in user interface

### Key Derivation Hierarchy
```
QKD Master Key (from quantum channel)
├── Level 2: HKDF-derived session keys (reusable)
├── Level 3: Direct consumption for OTP (one-time use)
└── Session Management: TTL and revocation policies
```

## Security Considerations

### Quantum Security Assessment
- **Level 0-1**: Vulnerable to quantum attacks
- **Level 2**: Quantum-enhanced but still relies on AES
- **Level 3**: Perfect secrecy - completely secure against any attack
- **Level 4**: Explicitly designed for post-quantum era
- **Level 5**: Variable security depending on algorithms used

### Performance vs Security Trade-offs
1. **Level 0**: Maximum performance, no security
2. **Level 1**: High performance, basic security
3. **Level 2**: High performance, quantum-enhanced security (recommended)
4. **Level 3**: Moderate performance, perfect security
5. **Level 4**: Moderate performance, future-proof security
6. **Level 5**: Variable performance, legacy compatibility

### Recommended Usage Guidelines

#### For Business Communications
- **Default**: Level 2 (Quantum-aided AES)
- **Sensitive**: Level 3 (OTP for critical messages)
- **Routine**: Level 1 (standard encryption)
- **Public**: Level 0 (no encryption)

#### For Personal Communications
- **Private**: Level 2 (quantum-aided)
- **Confidential**: Level 3 (perfect secrecy)
- **Casual**: Level 1 (standard)
- **Public**: Level 0 (none)

## Implementation Status

### Current Implementation
✅ **Level 0**: No encryption - implemented
✅ **Level 1**: Standard AES-256-GCM - implemented
✅ **Level 2**: Quantum-aided AES - implemented
✅ **Level 3**: One-Time Pad - implemented
✅ **Level 4**: Post-Quantum (placeholder) - implemented
✅ **Level 5**: Legacy TLS/PGP - implemented

### Crypto Module Support
✅ **AES-256-GCM**: Full implementation in Rust
✅ **HKDF**: Key derivation implementation
✅ **One-Time Pad**: XOR encryption implementation
✅ **Random Generation**: Cryptographically secure random bytes
⚠️ **CRYSTALS-Kyber**: Placeholder implementation (production needs liboqs)

### Key Management Service
✅ **Multi-level key generation**: All levels supported
✅ **QKD integration**: Simulated quantum key distribution
✅ **Session management**: TTL, revocation, usage tracking
✅ **Audit logging**: Complete security event tracking

## Configuration Examples

### UI Security Level Selector
```typescript
const SECURITY_LEVELS = [
  { value: 0, label: "No Encryption", description: "Standard email" },
  { value: 1, label: "Standard", description: "AES-256 encryption" },
  { value: 2, label: "Quantum-aided", description: "Quantum-enhanced AES (recommended)" },
  { value: 3, label: "Quantum Secure", description: "One-Time Pad (perfect secrecy)" },
  { value: 4, label: "Post-Quantum", description: "Future-proof encryption" },
  { value: 5, label: "Legacy", description: "TLS/PGP compatibility" }
];
```

### API Request Examples
```bash
# Level 2: Quantum-aided AES
curl -X POST http://localhost:8000/emails/send \
  -H "Authorization: Bearer $TOKEN" \
  -d '{"to": "aryan@example.com", "subject": "Test", "message": "Hello", "security_level": 2}'

# Level 3: One-Time Pad
curl -X POST http://localhost:8000/emails/send \
  -H "Authorization: Bearer $TOKEN" \
  -d '{"to": "aryan@qbiq.com", "subject": "Secret", "message": "Confidential", "security_level": 3}'
```

## Migration from Previous Implementation

### Security Level Mapping
| Old Level | New Level | Description |
|-----------|-----------|-------------|
| Level 1 (was OTP) | Level 3 | One-Time Pad moved to correct position |
| Level 2 | Level 2 | Quantum-aided AES (unchanged) |
| Level 3 (was PQC) | Level 4 | Post-Quantum Cryptography |
| Level 4 (was Legacy) | Level 5 | Legacy TLS/PGP |
| N/A | Level 0 | New: No encryption |
| N/A | Level 1 | New: Standard encryption |

This specification ensures that the quieo system correctly implements the original requirements while providing a clear path for future enhancements and quantum-ready communication.