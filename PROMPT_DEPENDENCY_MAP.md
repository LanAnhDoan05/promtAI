# SƠ ĐỒ PHỤ THUỘC PROMPT (PROMPT DEPENDENCY MAP)
## MẠNG LƯỚI QUAN HỆ & ĐƯỜNG GĂNG (CRITICAL PATH)

---

## 1. ĐƯỜNG GĂNG THI CÔNG DỰ ÁN (CRITICAL PATH)
```
PROMPT_001 (Khảo sát)
   └──> PROMPT_004 (Kiến trúc C4)
          └──> PROMPT_011 (Monorepo Init)
                 └──> PROMPT_012 (Express Backend) & PROMPT_013 (Next.js Frontend)
                        └──> PROMPT_019 (Prisma ORM Init)
                               └──> PROMPT_020 -> 029 (29 Prisma Models)
                                      └──> PROMPT_030 (Migration & Seed)
                                             └──> PROMPT_031 -> 048 (Backend Core APIs)
                                                    └──> PROMPT_049 -> 062 (Frontend UI Design)
                                                           └──> PROMPT_063 -> 078 (E-Commerce Features)
                                                                  ├──> PROMPT_079 -> 093 (AI Stylist Agent)
                                                                  ├──> PROMPT_094 -> 105 (Admin & AI BI)
                                                                  └──> PROMPT_106 -> 113 (VNPAY Integration)
                                                                         └──> PROMPT_114 -> 121 (Testing & Security)
                                                                                └──> PROMPT_122 -> 128 (Production & Signoff)
```

---

## 2. MA TRẬN PHỤ THUỘC GIỮA CÁC GIAI ĐOẠN
| Mã Giai Đoạn | Tên Giai Đoạn | Phụ thuộc trực tiếp vào | Mở khóa cho |
| :--- | :--- | :--- | :--- |
| **Phase 00** | Project Foundation | Thư mục dự án trống | Phase 01 |
| **Phase 01** | Environment Setup | Phase 00 (Prompt 010 Gateway) | Phase 02, Phase 04 |
| **Phase 02** | Database Architecture | Phase 01 (Prompt 018 Gateway) | Phase 03 |
| **Phase 03** | Backend Development | Phase 02 (Prompt 030 Gateway) | Phase 05, Phase 06, Phase 07, Phase 08 |
| **Phase 04** | Frontend Design | Phase 01 (Prompt 018 Gateway) | Phase 05 |
| **Phase 05** | E-commerce Features | Phase 03 & Phase 04 | Phase 06, Phase 07, Phase 08 |
| **Phase 06** | AI Stylist Agent | Phase 03 & Phase 05 | Phase 07 (Leads Handoff), Phase 09 |
| **Phase 07** | Admin & CRM | Phase 03, Phase 05 & Phase 06 | Phase 09 |
| **Phase 08** | Payment VNPay | Phase 03 & Phase 05 | Phase 09 |
| **Phase 09** | Testing & Security | Toàn bộ Phase 01 -> 08 | Phase 10 |
| **Phase 10** | Deployment Finalization| Phase 09 (Prompt 121 Gateway) | Nghiệm thu Go-Live |