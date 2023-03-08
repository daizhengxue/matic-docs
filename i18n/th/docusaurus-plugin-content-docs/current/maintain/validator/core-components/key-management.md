---
id: key-management
title: การจัดการ คีย์
description: การจัดการคีย์ผู้ลงนามและจัดการคีย์ของเจ้าของ
keywords:
  - docs
  - polygon
  - matic
  - key
  - key management
  - signer
  - owner
slug: key-management
image: https://wiki.polygon.technology/img/polygon-wiki.png
---

ตัวตรวจสอบความถูกต้องแต่ละตัวใช้คีย์สองชนิดในการจัดการกิจกรรมเกี่ยวกับตัวตรวจสอบความถูกต้องบน Polygon:

* คีย์ของผู้ลงนาม
* คีย์เจ้าของ

## คีย์ของผู้ลงนาม {#signer-key}

คีย์ของผู้ลงนามเป็นที่อยู่ที่ใช้เพื่อลงนามในบล็อก Heimdall, เช็คพอยต์และกิจกรรมที่เกี่ยวกับการลงนาม

คีย์ส่วนตัวของที่อยู่ของผู้ลงนามต้องอยู่ในเครื่องซึ่งกำลังเรียกใช้โหนดผู้ตรวจสอบความถูกต้องเพื่อวัตถุประสงค์ในการลงนาม

คีย์ของผู้ลงนามไม่สามารถนำมาใช้เพื่อจัดการการ Stake, ผลตอบแทน หรือการมอบหมาย

ผู้ตรวจสอบต้องเก็บ ETH ไว้ในที่อยู่ของผู้ลงนามใน Ethereum Mainnet เพื่อส่ง [เช็คพอยต์](/docs/maintain/glossary.md#checkpoint-transaction)

## คีย์ของเจ้าของ {#owner-key}

คีย์ของเจ้าของเป็นที่อยู่ที่ใช้ในการ Stake, Stake ใหม่อีกครั้ง, เปลี่ยนคีย์ของผู้ลงนาม, ถอนผลตอบแทน และจัดการพารามิเตอร์ที่เกี่ยวกับการมอบหมายสิทธิ์ใน Ethereum Mainnet คีย์ส่วนตัวสำหรับเจ้าของจะต้องปลอดภัยในทุกธุรกรรม

ธุรกรรมทั้งหมดซึ่งดำเนินการผ่านการใช้คีย์ของเจ้าของถูกดำเนินการใน Ethereum Mainnet

คีย์ของผู้ลงนามจะถูกเก็บไว้ในโหนด และโดยทั่วไปถือว่าเป็นกระเป๋าเงินแบบ**ร้อน** และคีย์ของเจ้าของจะต้องได้รับการรักษาความปลอดภัยอย่างเคร่งครัด ไม่ได้ใช้บ่อย และโดยทั่วไปถือว่าเป็นกระเป๋าเงินแบบ**เย็น** ทุนที่มีการ Stake จะถูกควบคุมโดยคีย์ของเจ้าของ

การแยกความรับผิดชอบระหว่างผู้ลงนามและคีย์ของเจ้าของที่ทำขึ้นนี้ ก็เพื่อให้แน่ใจถึงการแลกเปลี่ยนอย่างมีประสิทธิภาพระหว่างการรักษาความปลอดภัยและความสะดวกในการใช้งาน

คีย์ทั้งสองอันเป็นที่อยู่ที่เข้ากันได้กับ Ethereum และทำงานในลักษณะเดียวกันทุกประการ

## การเปลี่ยนผู้ลงนาม {#signer-change}

ดูที่ [เปลี่ยนที่อยู่ผู้ลงนามของคุณ](/docs/maintain/validate/change-signer-address)