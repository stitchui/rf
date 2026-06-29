# Risk Factor Mappings – UI Wireframes

## Default State

```text
Risk Factor Mappings                                  [+ Create]

IR
 └── Base
      └── OTC
           └── AED
                └── Swap (21)                      ⋮
```

---

## Action Menu

```text
Swap (21)                                          ⋮
                                                   ┌─────────┐
                                                   │ Edit    │
                                                   │ Archive │
                                                   └─────────┘
```

---

## Edit Mode

```text
Swap (21)                         [Cancel] [Save Disabled]
```

---

## Edit Mode After Changes

```text
Swap (21)                                  [Cancel] [Save]
```

---

## Grid Example

```text
Name                     Clearing House  Term Code  Shock Type  Tenor

USSTS.IR_AED_Swap.2M          LCH            2M      Absolute      1
USSTS.IR_AED_Swap.3Y          LCH            3Y      Absolute      1
USSTS.IR_AED_Swap.5Y          LCH            5Y      Absolute      1
```

---

## Archive Confirmation

```text
Archive Curve

Are you sure you want to archive curve "Swap"
and all related rows?

[Cancel] [Archive]
```

---

## Create Modal

```text
Create Risk Factor

Class      [ IR ▼ ]
Subclass   [ Base ▼ ]
Type       [ OTC ▼ ]
Curve      [ Swap ▼ ]

☑ USSTS.IR_AED_Swap.2M
☑ USSTS.IR_AED_Swap.3Y
☑ USSTS.IR_AED_Swap.5Y
☑ USSTS.IR_AED_Swap.10Y
☑ USSTS.IR_AED_Swap.25Y

[Cancel] [Create]
```

---

## Recommended Flow

```text
Default:
Swap (21)                                  ⋮

Edit:
Swap (21)                   [Cancel] [Save Disabled]

Changes Made:
Swap (21)                            [Cancel] [Save]

After Save:
Swap (21)                                  ⋮
```


<img width="1620" height="971" alt="image" src="https://github.com/user-attachments/assets/3eb7b028-335b-4af4-800e-0d95a70649b3" />
