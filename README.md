# ZATCA Phase 1 & Phase 2 TLV QR Code Helper (PHP / Laravel)

Lightweight, zero-dependency PHP 8.2+ / Laravel Tag-Length-Value (TLV) Base64 QR encoder for Saudi Arabian ZATCA (Fatoora) simplified and B2B tax invoices, maintained by [MTM4WEB](https://www.mtm4web.com/en).

---

## Features

- Generates ZATCA-compliant Base64 TLV strings (Tags 1–5 for Phase 1, extensible for Tags 6–9 XML invoice hash, ECDSA signature, and cryptographic stamp in Phase 2).
- Pure UTF-8 multi-byte safe byte-length calculation (`strlen()` on UTF-8 bytes) supporting Arabic seller names.
- Framework-agnostic PHP helper ready for Laravel 10/11 service providers and RESTful e-commerce backends.

---

## Quick Usage (PHP 8.2+)

```php
<?php

function encodeZatcaTlv(array $tags): string
{
    $tlv = '';
    foreach ($tags as $tag => $value) {
        $valueStr = (string) $value;
        $tlv .= pack('C', $tag) . pack('C', strlen($valueStr)) . $valueStr;
    }

    return base64_encode($tlv);
}

$qrPayload = encodeZatcaTlv([
    1 => 'MTM4WEB Digital Solutions',
    2 => '310123456700003',
    3 => '2026-11-21T19:00:00Z',
    4 => '1150.00',
    5 => '150.00',
]);
```

---

## Related Engineering Resources & Free Tools

- Full implementation guide: [ZATCA Phase 2 E-Invoicing Integration Guide for Saudi Stores](https://www.mtm4web.com/en/blog/zatca-phase-2-e-invoicing-integration-saudi-guide)
- Test your invoice QR payload online: [MTM4WEB Free QR Code Generator](https://www.mtm4web.com/en/qr-code-generator)
- Custom enterprise Laravel engineering: [Laravel Web & ERP Systems — MTM4WEB](https://www.mtm4web.com/en/laravel)
- Free web diagnostics & TTFB/DNS benchmarks: [MTM4WEB Free Developer & SEO Tools](https://www.mtm4web.com/en/tools)

---

*Built and open-sourced by [MTM4WEB](https://www.mtm4web.com/en) — Custom Laravel Development, E-Commerce & Technical SEO for Egypt, Saudi Arabia & UAE.*
