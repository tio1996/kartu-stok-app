# kartu-stok-appimport { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Table, TableHeader, TableRow, TableHead, TableBody, TableCell } from "@/components/ui/table";

export default function StockCardApp() {
  const [entries, setEntries] = useState([]);
  const [form, setForm] = useState({
    tanggal: "",
    kode: "",
    nama: "",
    satuan: "",
    masuk: 0,
    keluar: 0,
    keterangan: "",
  });

  const handleChange = (e) => {
    const { name, value } = e.target;
    setForm((prev) => ({ ...prev, [name]: value }));
  };

  const handleAdd = () => {
    const prevStok = entries.length ? entries[entries.length - 1].stokAkhir : 0;
    const stokAkhir = prevStok + Number(form.masuk) - Number(form.keluar);
    setEntries([...entries, { ...form, masuk: Number(form.masuk), keluar: Number(form.keluar), stokAkhir }]);
    setForm({ tanggal: "", kode: "", nama: "", satuan: "", masuk: 0, keluar: 0, keterangan: "" });
  };

  return (
    <div className="p-6 max-w-5xl mx-auto">
      <Card className="mb-6">
        <CardContent className="grid grid-cols-2 gap-4 p-4">
          <Input name="tanggal" type="date" value={form.tanggal} onChange={handleChange} placeholder="Tanggal" />
          <Input name="kode" value={form.kode} onChange={handleChange} placeholder="Kode Barang" />
          <Input name="nama" value={form.nama} onChange={handleChange} placeholder="Nama Barang" />
          <Input name="satuan" value={form.satuan} onChange={handleChange} placeholder="Satuan" />
          <Input name="masuk" type="number" value={form.masuk} onChange={handleChange} placeholder="Masuk" />
          <Input name="keluar" type="number" value={form.keluar} onChange={handleChange} placeholder="Keluar" />
          <Input name="keterangan" value={form.keterangan} onChange={handleChange} placeholder="Keterangan" />
          <div className="col-span-2">
            <Button onClick={handleAdd}>Tambah Transaksi</Button>
          </div>
        </CardContent>
      </Card>

      <Card>
        <CardContent className="p-4">
          <Table>
            <TableHeader>
              <TableRow>
                <TableHead>Tanggal</TableHead>
                <TableHead>Kode</TableHead>
                <TableHead>Nama</TableHead>
                <TableHead>Satuan</TableHead>
                <TableHead>Masuk</TableHead>
                <TableHead>Keluar</TableHead>
                <TableHead>Stok Akhir</TableHead>
                <TableHead>Keterangan</TableHead>
              </TableRow>
            </TableHeader>
            <TableBody>
              {entries.map((item, index) => (
                <TableRow key={index}>
                  <TableCell>{item.tanggal}</TableCell>
                  <TableCell>{item.kode}</TableCell>
                  <TableCell>{item.nama}</TableCell>
                  <TableCell>{item.satuan}</TableCell>
                  <TableCell>{item.masuk}</TableCell>
                  <TableCell>{item.keluar}</TableCell>
                  <TableCell>{item.stokAkhir}</TableCell>
                  <TableCell>{item.keterangan}</TableCell>
                </TableRow>
              ))}
            </TableBody>
          </Table>
        </CardContent>
      </Card>
    </div>
  );
}
