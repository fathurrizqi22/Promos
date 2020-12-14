### Fungsionalitas
- User dapat melakukan pemilihan menu makanan.
- User dapat menghapus makanan yang telah dipilih.

### How does it works?
Saat ingin membuka menu makanan button + telah dibuatkan sebuah method untuk mentrigger list item agar muncul seperti pada source code dibawah
```csharp
private void onButtonAddItemClicked(object sender, RoutedEventArgs e)
        {
            Penawaran penawaranWindow = new Penawaran();
            penawaranWindow.SetOnItemSelectedListener(this);
            penawaranWindow.Show();
        }
```
kemudian untuk melakukan penambahan item ke keranjang belanja dan menghitung sub total maka dibuatkan method seperti ini
```csharp
public void addItem(Item item)
        {
            this.itemBelanja.Add(item);
            this.callback.addItemSucceed();
            calculateSubTotal();
        }
```
untuk melakukan penghapusan item yang telah diambil dilakukan pada method `removeItem` di `KeranjangBelanja.cs`
```csharp
public void removeItem(Item item)
        {
            this.itemBelanja.Remove(item);
            this.callback.removeItemSucceed();
            calculateSubTotal();
        }
```
Untuk proses perhitungan total keseluruhan harga maka dilakukan perhitungan `subtotal + delivery fee - promo` seperti pada method dibawah ini
```csharp
 public void updateTotal(double subtotal)
        {
            double total = subtotal + deliveryFee - promo;
            this.balance = this.balance - total;
            this.paymentCallback.onPriceUpdated(subtotal,  total, balance);
        }

```