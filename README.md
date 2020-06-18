DATA: text(10) TYPE c VALUE '0123456789',
      text1(6) TYPE c,
      text2(6) TYPE c.

PARAMETERS position TYPE i.

CALL FUNCTION 'STRING_SPLIT_AT_POSITION'
     EXPORTING
          string            = text
          pos               = position
     IMPORTING
          string1           = text1
          string2           = text2
     EXCEPTIONS
          string1_too_small = 1
          string2_too_small = 2
          pos_not_valid     = 3
          OTHERS            = 4.

CASE sy-subrc.
  WHEN 0.
    WRITE: / text, / text1, / text2.
  WHEN 1.
    WRITE 'Target field 1 too short!'.
  WHEN 2.
    WRITE 'Target field 2 too short!'.
  WHEN 3.
    WRITE 'Invalid split position!'.
  WHEN 4.
    WRITE 'Other errors!'.
ENDCASE.
