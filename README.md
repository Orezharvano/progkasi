# programkasir
sebuah program aplikasi kasir
products = {
    1: ("Nasi Goreng", 15000),
    2: ("Mie Ayam", 12000),
    3: ("Ayam Geprek", 18000),
    4: ("Es Teh", 5000),
    5: ("Air Mineral", 4000)
}

cart = {}

print("=== PROGRAM KASIR ===")
customer = input("Masukkan nama customer: ")
print(f"Selamat datang, {customer}!\n")

# --- Tampilkan menu ---
def show_menu():
    print("\n=== MENU PRODUK ===")
    for pid, (name, price) in products.items():
        print(f"{pid}. {name:<12} - Rp{price}")

# --- Tampilkan keranjang ---
def show_cart():
    print("\n============ KERANJANG BELANJA ============")
    total = 0
    for pid, qty in cart.items():
        name, price = products[pid]
        subtotal = price * qty
        print(f"{name} x{qty} = Rp{subtotal}")
        total += subtotal
    print(f"TOTAL: Rp{total}")
    return total

# --- Input barang ---
while True:
    show_menu()
    pilih = input("Pilih ID barang (atau '6' untuk checkout): ")

    if pilih == "6":
        break

    try:
        pid = int(pilih)
        if pid not in products:
            print("ID barang tidak ditemukan.")
            continue

        qty = int(input("Jumlah: "))
        cart[pid] = cart.get(pid, 0) + qty
        print("Barang ditambahkan ke keranjang!\n")

    except ValueError:
        print("Input harus angka.")

# --- Checkout ---
if not cart:
    print("\nTidak ada barang di keranjang.")
else:
    total = show_cart()
    bayar = int(input("Jumlah uang customer: "))

    if bayar >= total:
        print("Kembalian:", bayar - total)
        print(f"\nTerima kasih, {customer}!")
    else:
        print("Uang tidak cukup!")
