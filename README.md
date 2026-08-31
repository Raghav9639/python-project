print("="*50)
print("SMARTCAMPUS UTILITY & ACCESS PASS")
print("="*50)

# ---- NEW MODIFIED VALUES ----
UG_FEE, PG_FEE = 650, 450
RES_FEE, VIS_FEE = 1100, 1500
PARK_2W, PARK_4W, EXTRA = 250, 700, 200
D1, D2, D3 = 0.25, 0.12, 0.20
R1, R2, R3, R4 = 4, 6, 9, 12
F1, F2, F3, F4 = 60, 130, 210, 350
# -----------------------------

cat = int(input("Category (1:Student, 2:Faculty): "))
base = disc = 0

if cat == 1:
    sub = input("Sub (UG/PG): ").upper().strip()
    if sub == "UG": base = UG_FEE
    elif sub == "PG": base = PG_FEE
    else: print("[ERROR] Invalid Student Type"); exit()
    cgpa = float(input("CGPA (0-10): "))
    if not 0 <= cgpa <= 10:
        print("[ERROR] Invalid CGPA"); exit()
    if cgpa >= 8.5: disc = base * D1
    elif cgpa >= 7.5: disc = base * D2
elif cat == 2:
    ftype = int(input("Faculty Type (1:Resident, 2:Visiting): "))
    if ftype == 1: base = RES_FEE
    elif ftype == 2: base = VIS_FEE
    else: print("[ERROR] Invalid Faculty Type"); exit()
    yrs = int(input("Years of Service: "))
    if yrs < 0: print("[ERROR] Invalid Year"); exit()
    if yrs > 10: disc = base * D3
else:
    print("[ERROR] Invalid Category"); exit()

park = int(input("Parking (0:None, 2:2W, 4:4W): "))
park_fee = extra = 0
if park == 0: park_fee = 0
elif park == 2: park_fee = PARK_2W
elif park == 4:
    park_fee = PARK_4W
    if cat == 1: extra = EXTRA
else: print("[ERROR] Invalid Parking"); exit()

units = float(input("Electricity Units: "))
if units < 0: print("[ERROR] Invalid Units"); exit()

if units <= 100:
    bill = units * R1; fix = F1
elif units <= 300:
    bill = 100*R1 + (units-100)*R2; fix = F2
elif units <= 500:
    bill = 100*R1 + 200*R2 + (units-300)*R3; fix = F3
else:
    bill = 100*R1 + 200*R2 + 200*R3 + (units-500)*R4; fix = F4

e_total = bill + fix
net = base - disc + park_fee + extra
total = net + e_total

print("\n" + "="*60)
print("INVOICE BREAKDOWN")
print("="*60)
print(f"Base Fee : ₹{base:.2f} | Discount : -₹{disc:.2f}")
print(f"Parking : ₹{park_fee:.2f} | Extra : ₹{extra:.2f}")
print("-"*60)
print(f"Net Pass Total : ₹{net:.2f}")
print(f"Electricity : ₹{bill:.2f} + Fixed ₹{fix:.2f} = ₹{e_total:.2f}")
print("="*60)
print(f"TOTAL PAYABLE : ₹{total:.2f}")
print("="*60)
