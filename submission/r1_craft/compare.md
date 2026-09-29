# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_006840.jpg
- L8 mid IGNORE_SCOPE
- L7+R6 mid BOX_GEOMETRY
- R4 center MISSING
## adasind_036720.jpg
## adasind_056040.jpg
- L7+R7 mid WRONG_CLASS

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 10 | 9 | 1 | 0 |
| mid | 7 | 5 | 2 | 2 |
| edge | 3 | 3 | 0 | 0 |
