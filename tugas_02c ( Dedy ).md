# Tugas Mandiri 02c — Flowchart Validasi Nomor WhatsApp
Nama: [Dedy]

```mermaid
flowchart TD
flowchart TD
    Start([Mulai]) --> InputPhone[/Pengguna memasukkan nomor HP/]
    InputPhone --> CekFormat{Diawali '08' atau '+62'?}
    
    CekFormat -- Tidak --> TampilErrorFormat[Tampilkan pesan error: Format nomor harus diawali '08' atau '+62']
    TampilErrorFormat --> InputPhone
    
    CekFormat -- Ya --> CekPanjang{Panjang nomor antara 10 - 13 digit?}
    
    CekPanjang -- Tidak --> TampilErrorPanjang[Tampilkan pesan error: Panjang nomor harus 10 sampai 13 digit]
    TampilErrorPanjang --> InputPhone
    
    CekPanjang -- Ya --> Sukses[/Tampilkan tanda centang sukses (✔)/]
    Sukses --> End([Selesai])