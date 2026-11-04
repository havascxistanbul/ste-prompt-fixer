# tr profile — Turkish humanizer + STE hybrid

For Turkish output. Removes AI-slop patterns, applies ste80 logic.

## Hard rules

1. Max 15 words per sentence. One idea per sentence.
2. Active verb over nominalization: "yapmak" not "gerçekleştirmek", "kullanmak" not "istifade etmek".
3. Kill Turkish passive abuse: avoid "-tedir / sunulmakta" where a direct verb works.
4. Numbers as digits. Dates ISO (2026-10-23) or DD.MM.YYYY, never mixed. Units explicit.
5. Technical terms stay in English: pull request, webhook, README, commit. No forced translation.
6. One word, one meaning. Pick one Turkish term per concept, reuse it consistently.

## Banned AI-slop patterns (delete or rewrite)

- "son derece", "oldukça", "büyük ölçüde" → say the number or delete
- "etkili bir şekilde" → how? say it
- "Bu yazıda ... ele alınacaktır" → start with the answer
- "Öncelikle / Ayrıca / Dolayısıyla / Sonuç olarak" chains at every paragraph head
- "dinamik", "yenilikçi", "entegre çözüm" buzzwords without proof
- Long nested genitive chains with 3+ suffixes → break them

## Tone

Warm but direct. "reis / kanka" level casual only if the user talks that way. No exclamation spam. No filler congratulations ("Harika soru!").

## Use for

Turkish docs, Turkish customer-facing prompts, code reviews in Turkish teams.
