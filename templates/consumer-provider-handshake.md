# Consumer–Provider Handshake

## Thông tin chung

- Lab: FIT4110 Lab 03
- Ngày: 2026-05-25
- Provider team: AI Vision (Nhóm AI)
- Consumer team: Core Business (Nhóm 12)
- Provider service: AI Vision Service
- Consumer service: Core Business Service

## Contract

- Contract file: `contracts/ai-vision.openapi.yaml`
- Mock base URL: `http://localhost:4011`
- Auth method: Bearer Token (`lab-token`)
- Endpoint được test: `POST /vision/face-match`

## Smoke test

### Request

```http
POST /vision/face-match
Authorization: Bearer lab-token
Content-Type: application/json
```

```json
{
  "requestType": "IMAGE_REF",
  "traceId": "0196fb3d-4ad7-7d1e-9f49-5d5148d2babc",
  "imageRef": "https://storage.campus.local/frames/frame-001.jpg"
}
```

### Expected response

```json
{
  "matchId": "0196fb3d-4ad7-7d1e-9f49-5d5148d2babc",
  "traceId": "0196fb3d-4ad7-7d1e-9f49-5d5148d2babc",
  "decision": "MATCH",
  "confidence": 0.97,
  "subjectId": "STUDENT-2026-001",
  "reason": null,
  "modelVersion": "v2.1.0",
  "processedAt": "2026-05-10T08:00:00Z"
}
```

## Kết quả

- [x] Consumer gọi mock thành công.
- [x] Consumer parse được field cần dùng.
- [x] Consumer hiểu lỗi 4xx/5xx provider trả về.
- [x] Có Newman report hoặc screenshot.

## Ghi chú thay đổi hợp đồng

| Nội dung | Trước | Sau | Người đồng ý |
|---|---|---|---|
| Cấu trúc FaceMatchRequest | Chưa hỗ trợ Embedding | Dùng oneOf với requestType là discriminator | Nguyễn Công Hiệp |
| Thang đo confidence | 0-100 | Float 0.0 - 1.0 | Đỗ Trung Kiên |
| Decision LOW_CONFIDENCE | Không có | Thêm status LOW_CONFIDENCE trả về 200 | Đỗ Trung Kiên |

## Xác nhận

- Provider representative: Đỗ Trung Kiên (AI Vision Team)
- Consumer representative: Nguyễn Công Hiệp (Core Business - Nhóm 12)
