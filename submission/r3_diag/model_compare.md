# L / R / M

L/R/M là thứ tự box in-scope theo XML của từng frame.

## adasind_006840.jpg
- L1+R1: LR_noM (center)
- L2+R7: LR_noM (mid)
- L3+R8+M1: LRM (center)
- L9+R9+M11: LRM (edge)
- L5+R5+M7: LRM (mid)
- L4+R2+M2: LRM (mid)
- L6+R3+M5: LRM (center)
- L7: L_only (mid)
- R4: R_only (center)
- R6: R_only (mid)
- M3: M_only (mid)
- M6: M_only (center)
- M8: M_only (mid)
- M9: M_only (center)
- M10: M_only (mid)
- M12: M_only (center)
- M13: M_only (center)
## adasind_036720.jpg
- L4+R4: LR_noM (edge)
- L1+R1: LR_noM (mid)
- L2+R3: LR_noM (center)
- L3+R2+M3: LRM (center)
- M1: M_only (edge)
- M2: M_only (edge)
- M4: M_only (center)
- M6: M_only (edge)
## adasind_056040.jpg
- L5+R5: LR_noM (center)
- L2+R2: LR_noM (edge)
- L4+R3+M7: LRM (center)
- L3+R4: LR_noM (center)
- L6+R6+M8: LRM (mid)
- L1+R1+M1: LRM (center)
- L7: L_only (mid)
- R7+M6: RM_noL (mid)
- M2: M_only (edge)
- M3: M_only (edge)
- M4: M_only (mid)
- M5: M_only (center)
- M9: M_only (mid)
- M11: M_only (mid)

## Zone × cell
| zone | LRM | LR_noM | LM_noR | L_only | RM_noL | R_only | M_only |
|---|---|---|---|---|---|---|---|
| center | 5 | 4 | 0 | 0 | 0 | 1 | 6 |
| mid | 3 | 2 | 0 | 2 | 1 | 1 | 6 |
| edge | 1 | 2 | 0 | 0 | 0 | 0 | 5 |
