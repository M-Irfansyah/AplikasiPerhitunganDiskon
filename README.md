# AplikasiPerhitunganDiskon
 Tugas 3 - M.irfansyah(2210010176)

## Deskripsi Program
• Pengguna memasukkan harga asli dan memilih persentase diskon

• Setelah menghitung, tampilkan harga akhir dan jumlah penghematan

## Komponen GUI
JFrame, JPanel, JLabel, JTextField, JComboBox, JButton , JSlider
- JLabel untuk judul aplikasi, seperti "Aplikasi Perhitungan Diskon".
- JLabel untuk label "Harga Asli", JTextField untuk input harga asli (beri nama txtHargaAsli).
- JLabel untuk label "Persentase Diskon", JComboBox (beri nama comboDiskon) untuk pilihan persentase diskon (10%, 20%, 30%, dst.).
- JButton dengan teks "Hitung" dan nama btnHitung.
- JLabel untuk label "Harga Akhir" dan JTextField (beri nama txtHargaAkhir) untuk menampilkan hasil harga akhir (set Editable menjadi false).
- JLabel untuk label "Penghematan" dan JTextField (beri nama txtPenghematan) untuk menampilkan jumlah penghematan (set Editable menjadi false).
- JSlider juga untuk untuk pilihan persentase diskon dan hasil persentase akan tampil di JLabel lblDiskonSlider

## Logika Program
Perhitungan aritmatika, Penanganan eksepsi

## Events
• ActionListener untuk tombol Hitung
``` 
private void btnHitungActionPerformed(java.awt.event.ActionEvent evt) {                                          
    try {
            // Cek apakah hargaAsliTextField kosong atau tidak valid
            if (hargaAsli.getText().isEmpty() || hargaAsli.getText().equals("Rp ")) {
                JOptionPane.showMessageDialog(this, "Silakan masukkan harga asli.", "Error", JOptionPane.ERROR_MESSAGE);
                return;
            }

            // Ambil harga asli dari JTextField dan hilangkan "Rp " di depannya
            double HargaAsli = Double.parseDouble(hargaAsli.getText().replace("Rp ", ""));

            // Tentukan diskon persentase dari JSlider atau JComboBox
            int diskonPersen;
            if (diskonSlider.getValue() > 0) {
                diskonPersen = diskonSlider.getValue();
            } else {
                String diskonStr = (String) diskon.getSelectedItem();
                diskonPersen = Integer.parseInt(diskonStr.replace("%", ""));
            }

            // Ambil kode kupon dari JTextField
            String KodeKupon = kuponDiskon.getText().trim();

            // Tambahan diskon jika kode kupon valid
            if (KodeKupon.equalsIgnoreCase("tugas3")) {
                diskonPersen += 10;
                JOptionPane.showMessageDialog(this, "Kode kupon 10% berhasil diterapkan!", "Info", JOptionPane.INFORMATION_MESSAGE);
            } else if (!KodeKupon.isEmpty()) {
                JOptionPane.showMessageDialog(this, "Kode kupon tidak valid.", "Info", JOptionPane.INFORMATION_MESSAGE);
            }

            // Hitung penghematan dan harga akhir
            double Penghematan = HargaAsli * diskonPersen / 100;
            double HargaAkhir = HargaAsli - Penghematan;

            // Tampilkan hasil pada JTextField dengan prefix "Rp "
            penghematan.setText("Rp " + String.format("%.2f", Penghematan));
            hargaAkhir.setText("Rp " + String.format("%.2f", HargaAkhir));

            // Tambahkan hasil ke riwayat
            String hasilRiwayat = "Harga Asli: Rp " + HargaAsli +
                                  ", Diskon: " + diskonPersen + "%" +
                                  ", Penghematan: Rp " + String.format("%.2f", Penghematan) +
                                  ", Harga Akhir: Rp " + String.format("%.2f", HargaAkhir) + "\n";
            jTextArea1.append(hasilRiwayat);
        } catch (NumberFormatException e) {
            JOptionPane.showMessageDialog(this, "Masukkan nilai yang valid.", "Error", JOptionPane.ERROR_MESSAGE);
        }    // TODO add your handling code here:
    } 
```            
• ItemListener pada JComboBox untuk memilih persentase diskon
```
public PerhitunganDiskonFrame() {
        initComponents();
        diskon.addItem("10%");        
        diskon.addItem("20%");        
        diskon.addItem("30%");
        diskon.addItem("40%");
    }
```

## Variasi
• Tambahkan opsi untuk memasukkan kode kupon diskon tambahan
```
 String KodeKupon = kuponDiskon.getText().trim();

            // Tambahan diskon jika kode kupon valid
            if (KodeKupon.equalsIgnoreCase("tugas3")) {
                diskonPersen += 10;
                JOptionPane.showMessageDialog(this, "Kode kupon 10% berhasil diterapkan!", "Info", JOptionPane.INFORMATION_MESSAGE);
            } else if (!KodeKupon.isEmpty()) {
                JOptionPane.showMessageDialog(this, "Kode kupon tidak valid.", "Info", JOptionPane.INFORMATION_MESSAGE);
            }
```
• Tambahkan JSlider sebagai alternatif JComboBox untuk memilih persentase diskon
```
// Tentukan diskon persentase dari JSlider atau JComboBox
            int diskonPersen;
            if (diskonSlider.getValue() > 0) {
                diskonPersen = diskonSlider.getValue();
            } else {
                String diskonStr = (String) diskon.getSelectedItem();
                diskonPersen = Integer.parseInt(diskonStr.replace("%", ""));
            }
```
• Sediakan riwayat perhitungan diskon yang telah dilakukan.
```
double Penghematan = HargaAsli * diskonPersen / 100;
            double HargaAkhir = HargaAsli - Penghematan;

            // Tampilkan hasil pada JTextField dengan prefix "Rp "
            penghematan.setText("Rp " + String.format("%.2f", Penghematan));
            hargaAkhir.setText("Rp " + String.format("%.2f", HargaAkhir));

            // Tambahkan hasil ke riwayat
            String hasilRiwayat = "Harga Asli: Rp " + HargaAsli +
                                  ", Diskon: " + diskonPersen + "%" +
                                  ", Penghematan: Rp " + String.format("%.2f", Penghematan) +
                                  ", Harga Akhir: Rp " + String.format("%.2f", HargaAkhir) + "\n";
            jTextArea1.append(hasilRiwayat);
        } catch (NumberFormatException e) {
            JOptionPane.showMessageDialog(this, "Masukkan nilai yang valid.", "Error", JOptionPane.ERROR_MESSAGE);
        }
```

## Contoh Gambar Project Setelah di Run
![aplikasi diskon 4](https://github.com/user-attachments/assets/79f3e9b4-2907-4a83-bd5c-c38d9d0cf3ac)
![aplikasi diskon 3](https://github.com/user-attachments/assets/5badc3c4-8d19-4acf-9d18-c511e4c8777d)
![aplikasi diskon 2](https://github.com/user-attachments/assets/70a48b47-5b7d-4990-afeb-13feab9c02ee)
![aplikasi diskon 1](https://github.com/user-attachments/assets/95d66d6b-18eb-411e-88a9-20c721810e1b)


## Indikator Penilaian:

| No  | Komponen         |  Persentase  |
| :-: | --------------   |   :-----:    |
|  1  | Komponen GUI     |    20    |
|  2  | Logika Program   |    20    |
|  3  | Kesesuaian UI    |    15    |
|  4  | Constructor      |    15    |
|  5  | Memenuhi Variasi |    30    |
|     | TOTAL        | 100 |

## Pembuat

Nama  : M.Irfansyah

NPM   : 2210010176
