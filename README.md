# ScaleUP-MyFirstProject-
PLS,help me and tell me what i did wrong just in case
#PHYTON



import tkinter as tk
from tkinter import ttk
from tkinter import messagebox

def buat_jendela_konversi(judul, fields, konversi_fn):
    window = tk.Toplevel(root)
    window.title(judul)
    window.geometry("400x300")
    window.configure(bg="#1E1E2F")

    entries = {}

    for i, (label_text, satuan_opsi) in enumerate(fields):
        tk.Label(window, text=label_text, font=("Arial", 12, "bold"), bg="#1E1E2F", fg="white").grid(row=i, column=0, padx=10, pady=5)
        ent = tk.Entry(window, font=("Arial", 12), bg="#2A2A3D", fg="white", insertbackground="white")
        ent.grid(row=i, column=1, padx=10, pady=5)
        entries[label_text] = ent

        if satuan_opsi:
            var = tk.StringVar(window)
            var.set(satuan_opsi[0])
            cmb = ttk.Combobox(window, textvariable=var, values=satuan_opsi, font=("Arial", 11))
            cmb.grid(row=i, column=2, padx=10, pady=5)
            entries[label_text + "_unit"] = var

    result_label = tk.Label(window, text="Hasil akan ditampilkan di sini.", font=("Arial", 12, "bold"), bg="#1E1E2F", fg="#FF9500")
    result_label.grid(row=len(fields)+1, column=0, columnspan=3, pady=10)

    def hitung():
        try:
            result = konversi_fn(entries)
            result_label.config(text=result)
        except Exception as e:
            messagebox.showerror("Error", str(e))

    button_frame = tk.Frame(window, bg="#1E1E2F")
    button_frame.grid(row=len(fields)+2, column=0, columnspan=3, pady=10)
    
    konversi_btn = tk.Button(button_frame, text="Konversi", command=hitung,
                font=("Arial", 11, "bold"), bg="#007BFF", fg="white", 
                activebackground="#0056b3", activeforeground="white",
                relief="flat", padx=15, pady=5)
    konversi_btn.pack(side="left", padx=10)
    
    kembali_btn = tk.Button(button_frame, text="Kembali", command=window.destroy,
                font=("Arial", 11, "bold"), bg="#007BFF", fg="white",  
                activebackground="#0056b3", activeforeground="white",
                relief="flat", padx=15, pady=5)
    kembali_btn.pack(side="left", padx=10)

def settings():
    window = tk.Toplevel(root)
    window.title("Settings")
    window.geometry("400x300")
    window.configure(bg="#1E1E2F")

    tk.Label(window, text="Settings", font=("Arial", 16, "bold"), bg="#1E1E2F", fg="white").pack(pady=10)

    tk.Label(window, text="Credit:", font=("Arial", 12, "bold"), bg="#1E1E2F", fg="white").pack(anchor="w", padx=20, pady=5)
    tk.Label(window, text="Coder: skibidi85", font=("Arial", 12), bg="#1E1E2F", fg="white").pack(anchor="w", padx=40)
    tk.Label(window, text="Designer: sikibidi85", font=("Arial", 12), bg="#1E1E2F", fg="white").pack(anchor="w", padx=40)
    tk.Label(window, text="Time Creation: 03/05/2025", font=("Arial", 12), bg="#1E1E2F", fg="white").pack(anchor="w", padx=40)

    def toggle_mode():
        if root["bg"] == "#222222":  
            root.configure(bg="white")
            for widget in root.winfo_children():
                widget.configure(bg="white", fg="black")
        else:  
            root.configure(bg="#222222")
            for widget in root.winfo_children():
                widget.configure(bg="#222222", fg="white")

    mode_btn = tk.Button(window, text="Toggle Dark/Light Mode", command=toggle_mode,
                         font=("Arial", 12, "bold"), bg="#007BFF", fg="white",
                         activebackground="#0056b3", activeforeground="white",
                         relief="flat", padx=15, pady=5)
    mode_btn.pack(pady=20)

    kembali_btn = tk.Button(window, text="Kembali", command=window.destroy,
                            font=("Arial", 12, "bold"), bg="#007BFF", fg="white",
                            activebackground="#0056b3", activeforeground="white",
                            relief="flat", padx=15, pady=5)
    kembali_btn.pack(pady=10)

def suhu():
    window = tk.Toplevel(root)
    window.title("Konversi Suhu")
    window.geometry("350x300")
    window.configure(bg="#333333")

    frame = tk.Frame(window, bg="#333333", padx=20, pady=20)
    frame.pack(fill="both", expand=True)

    tk.Label(frame, text="Masukkan suhu:", font=("Arial", 12, "bold"), bg="#333333", fg="white").pack(pady=5)

    entry = tk.Entry(frame, font=("Arial", 12), bg="#444444", fg="white", insertbackground="white", justify="center")
    entry.pack(pady=10, fill="x")

    unit_frame = tk.Frame(frame, bg="#333333")
    unit_frame.pack(pady=10)

    var_satuan = tk.StringVar()
    var_satuan.set("C")
    
 
    units = [("Celsius (°C)", "C"), ("Fahrenheit (°F)", "F"), ("Kelvin (K)", "K")]
    for text, value in units:
        rb = tk.Radiobutton(unit_frame, text=text, variable=var_satuan, value=value,
                     font=("Arial", 11), bg="#333333", fg="white", 
                     selectcolor="#444444", activebackground="#333333", activeforeground="white")
        rb.pack(anchor="w", pady=2)

    hasil_label = tk.Label(frame, text="", font=("Arial", 12, "bold"), fg="#FF9500", bg="#333333")
    hasil_label.pack(pady=15)

    def konversi():
        try:
            nilai = float(entry.get())
            satuan = var_satuan.get()
            
            if satuan == "C":
                celsius = nilai
                fahrenheit = nilai * 9/5 + 32
                kelvin = nilai + 273.15
                hasil = f"F: {fahrenheit:.2f}°F, K: {kelvin:.2f}K"
            elif satuan == "F":
                celsius = (nilai - 32) * 5/9
                fahrenheit = nilai
                kelvin = (nilai - 32) * 5/9 + 273.15
                hasil = f"C: {celsius:.2f}°C, K: {kelvin:.2f}K"
            elif satuan == "K":
                celsius = nilai - 273.15
                fahrenheit = (nilai - 273.15) * 9/5 + 32
                kelvin = nilai
                hasil = f"C: {celsius:.2f}°C, F: {fahrenheit:.2f}°F"
            else:
                hasil = "Satuan tidak dikenali"
                
            hasil_label.config(text=hasil)
        except ValueError:
            hasil_label.config(text="Input tidak valid")

    button_frame = tk.Frame(frame, bg="#333333")
    button_frame.pack(pady=10)
    
    konversi_btn = tk.Button(button_frame, text="Konversi", command=konversi,
            font=("Arial", 11, "bold"), bg="#FF9500", fg="white", 
            activebackground="#FFB347", activeforeground="white",
            relief="flat", padx=15, pady=5)
    konversi_btn.pack(side="left", padx=10)

    kembali_btn = tk.Button(button_frame, text="Kembali", command=window.destroy,
            font=("Arial", 11, "bold"), bg="#666666", fg="white", 
            activebackground="#888888", activeforeground="white",
            relief="flat", padx=15, pady=5)
    kembali_btn.pack(side="left", padx=10)

def panjang():
    """Fungsi untuk membuka jendela konversi panjang"""
    satuan_panjang = ["mm","cm","dm","m","dam" ,"hm","km","inch","feet","yard","mile"]

    def konversi_panjang(entries):
        try:
            nilai = float(entries["Nilai"].get())
            dari = entries["Nilai_unit"].get()
            ke = entries["Konversi ke_unit"].get()
            
            nilai_dalam_meter = 0
            if dari == "mm":
                nilai_dalam_meter = nilai / 1000
            elif dari == "cm":
                nilai_dalam_meter = nilai / 100
            elif dari == "m":
                nilai_dalam_meter = nilai
            elif dari == "km":
                nilai_dalam_meter = nilai * 1000
            elif dari == "inch":
                nilai_dalam_meter = nilai * 0.0254
            elif dari == "feet":
                nilai_dalam_meter = nilai * 0.3048
            elif dari == "yard":
                nilai_dalam_meter = nilai * 0.9144
            elif dari == "mile":
                nilai_dalam_meter = nilai * 1609.34
            
            hasil = 0
            if ke == "mm":
                hasil = nilai_dalam_meter * 1000
            elif ke == "cm":
                hasil = nilai_dalam_meter * 100
            elif ke == "m":
                hasil = nilai_dalam_meter
            elif ke == "km":
                hasil = nilai_dalam_meter / 1000
            elif ke == "inch":
                hasil = nilai_dalam_meter / 0.0254
            elif ke == "feet":
                hasil = nilai_dalam_meter / 0.3048
            elif ke == "yard":
                hasil = nilai_dalam_meter / 0.9144
            elif ke == "mile":
                hasil = nilai_dalam_meter / 1609.34
            
            return f"{nilai} {dari} = {hasil:.6f} {ke}"
        except Exception as e:
            return f"Error: {str(e)}"

    fields = [
        ("Nilai", satuan_panjang),
        ("Konversi ke", satuan_panjang)
    ]

    buat_jendela_konversi("Konversi Satuan Panjang", fields, konversi_panjang)

def waktu():
    """Fungsi untuk membuka jendela konversi waktu"""
    satuan_waktu = ["detik", "menit", "jam", "hari", "minggu", "bulan", "tahun"]

    def konversi_waktu(entries):
        try:
            nilai = float(entries["Nilai"].get())
            dari = entries["Nilai_unit"].get()
            ke = entries["Konversi ke_unit"].get()
            
            nilai_dalam_detik = 0
            if dari == "detik":
                nilai_dalam_detik = nilai
            elif dari == "menit":
                nilai_dalam_detik = nilai * 60
            elif dari == "jam":
                nilai_dalam_detik = nilai * 3600
            elif dari == "hari":
                nilai_dalam_detik = nilai * 86400
            elif dari == "minggu":
                nilai_dalam_detik = nilai * 604800
            elif dari == "bulan":
                nilai_dalam_detik = nilai * 2592000
            elif dari == "tahun":
                nilai_dalam_detik = nilai * 31536000
            
            hasil = 0
            if ke == "detik":
                hasil = nilai_dalam_detik
            elif ke == "menit":
                hasil = nilai_dalam_detik / 60
            elif ke == "jam":
                hasil = nilai_dalam_detik / 3600
            elif ke == "hari":
                hasil = nilai_dalam_detik / 86400
            elif ke == "minggu":
                hasil = nilai_dalam_detik / 604800
            elif ke == "bulan":
                hasil = nilai_dalam_detik / 2592000
            elif ke == "tahun":
                hasil = nilai_dalam_detik / 31536000
            
            return f"{nilai} {dari} = {hasil:.6f} {ke}"
        except Exception as e:
            return f"Error: {str(e)}"

    fields = [
        ("Nilai", satuan_waktu),
        ("Konversi ke", satuan_waktu)
    ]

    buat_jendela_konversi("Konversi Satuan Waktu", fields, konversi_waktu)

def berat():
    satuan_berat = ["mg", "g", "kg", "ton", "ounce", "pound"]

    def konversi_berat(entries):
        try:
            nilai = float(entries["Nilai"].get())
            dari = entries["Nilai_unit"].get()
            ke = entries["Konversi ke_unit"].get()

            
            dalam_gram = {
                "mg": nilai / 1000,
                "g": nilai,
                "kg": nilai * 1000,
                "ton": nilai * 1_000_000,
                "ounce": nilai * 28.3495,
                "pound": nilai * 453.592
            }[dari]

            hasil = {
                "mg": dalam_gram * 1000,
                "g": dalam_gram,
                "kg": dalam_gram / 1000,
                "ton": dalam_gram / 1_000_000,
                "ounce": dalam_gram / 28.3495,
                "pound": dalam_gram / 453.592
            }[ke]

            return f"{nilai} {dari} = {hasil:.6f} {ke}"
        except Exception as e:
            return f"Error: {str(e)}"

    fields = [
        ("Nilai", satuan_berat),
        ("Konversi ke", satuan_berat)
    ]
    buat_jendela_konversi("Konversi Satuan Berat", fields, konversi_berat)

def luas():
    satuan_luas = ["mm²", "cm²", "m²", "km²", "are", "hektar"]

    def konversi_luas(entries):
        try:
            nilai = float(entries["Nilai"].get())
            dari = entries["Nilai_unit"].get()
            ke = entries["Konversi ke_unit"].get()

            dalam_m2 = {
                "mm²": nilai / 1e6,
                "cm²": nilai / 1e4,
                "m²": nilai,
                "km²": nilai * 1e6,
                "are": nilai * 100,
                "hektar": nilai * 10000
            }[dari]

            hasil = {
                "mm²": dalam_m2 * 1e6,
                "cm²": dalam_m2 * 1e4,
                "m²": dalam_m2,
                "km²": dalam_m2 / 1e6,
                "are": dalam_m2 / 100,
                "hektar": dalam_m2 / 10000
            }[ke]

            return f"{nilai} {dari} = {hasil:.6f} {ke}"
        except Exception as e:
            return f"Error: {str(e)}"

    fields = [
        ("Nilai", satuan_luas),
        ("Konversi ke", satuan_luas)
    ]
    buat_jendela_konversi("Konversi Satuan Luas", fields, konversi_luas)

def kalkulator():
    window = tk.Toplevel(root)
    window.title("Kalkulator")
    window.geometry("300x400")
    window.configure(bg="#333333")

    expression = tk.StringVar()

   
    entry = tk.Entry(window, textvariable=expression, font=("Arial", 20, "bold"), bd=0, 
                   relief="flat", justify="right", bg="#444444", fg="white", insertbackground="white")
    entry.pack(fill="both", padx=10, pady=10)

    def klik(t):
        if t == "=":
            try:
                result = str(eval(expression.get()))
                expression.set(result)
            except:
                expression.set("Error")
        elif t == "C":
            expression.set("")
        else:
            expression.set(expression.get() + str(t))

   
    tombol = [
        ['7', '8', '9', '/'],
        ['4', '5', '6', '*'],
        ['1', '2', '3', '-'],
        ['0', '.', '=', '+'],
        ['C']
    ]
    
    button_frame = tk.Frame(window, bg="#333333")
    button_frame.pack(expand=True, fill="both", padx=10, pady=10)
    
    
    for i in range(5):
        button_frame.rowconfigure(i, weight=1)
    for i in range(4):
        button_frame.columnconfigure(i, weight=1)

    for i, baris in enumerate(tombol):
        for j, t in enumerate(baris):
            if t == '=':
                bg_color = "#FF9500"  
                fg_color = "white"
            elif t in ['+', '-', '*', '/']:
                bg_color = "#666666"  
                fg_color = "white"
            elif t == 'C':
                bg_color = "#FF3B30"  
                fg_color = "white"
               
                b = tk.Button(button_frame, text=t, font=("Arial", 14, "bold"), fg=fg_color, bg=bg_color,
                          activebackground="#777777", activeforeground="white", relief="flat",
                          command=lambda t=t: klik(t))
                b.grid(row=i, column=0, columnspan=4, sticky="nsew", padx=2, pady=2)
                continue
            else:
                bg_color = "#444444"  
                fg_color = "white"
                
            b = tk.Button(button_frame, text=t, font=("Arial", 14, "bold"), fg=fg_color, bg=bg_color,
                          activebackground="#777777", activeforeground="white", relief="flat",
                          command=lambda t=t: klik(t))
            b.grid(row=i, column=j, sticky="nsew", padx=2, pady=2)

def main():
    global root
    root = tk.Tk()
    root.title("ScaleUP")
    root.geometry("700x500")
    root.configure(bg="#222222")  
    
  
    exit_btn = tk.Button(root, text="EXIT", command=root.destroy,
                      font=("Arial", 10, "bold"), bg="#FF3B30", fg="white",
                      activebackground="#FF6B6B", activeforeground="white",
                      relief="flat", padx=10, pady=5)
    exit_btn.place(x=20, y=20)
    
    
    title_label = tk.Label(root, text="SCALE UP", font=("Arial", 48, "bold"),
                        fg="white", bg="#222222")
    title_label.pack(pady=40)
    
    main_frame = tk.Frame(root, bg="#222222")
    main_frame.pack(expand=True, fill="both", padx=40, pady=10)
    
 
    for i in range(2):
        main_frame.rowconfigure(i, weight=1)
    for i in range(3):
        main_frame.columnconfigure(i, weight=1)
    
    
    buttons = [
        ("KONVERSI SUHU", suhu),
        ("KONVERSI BERAT", berat),
        ("KONVERSI LUAS", luas),
        ("KONVERSI WAKTU", waktu),
        ("KONVERSI PANJANG", panjang),
        ("KALKULATOR", kalkulator)
    ]
    
    
    for i, (text, command) in enumerate(buttons):
        row = i // 3
        col = i % 3
        
        frame = tk.Frame(main_frame, bg="#999999", bd=0, relief="flat")
        frame.grid(row=row, column=col, padx=10, pady=10, sticky="nsew")
        
        btn = tk.Button(frame, text=text, command=command,
                     font=("Arial", 12, "bold"), fg="#333333", bg="#999999",
                     activebackground="#BBBBBB", activeforeground="#333333",
                     bd=0, relief="flat")
        btn.pack(expand=True, fill="both")

    root.mainloop()

if __name__ == "__main__":
    main()
