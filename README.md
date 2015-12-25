# Android-BLE
  *** Android API: 18+ (Android 4.3+) ****

### BLE Permission
ขออนุญาติใช้งาน Bluetooth ตั้งค่าเพิ่มภายในไฟล์ AndroidManifest.xml
```java
<uses-permission android:name="android.permission.BLUETOOTH"/>
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN"/>

/* กำหนดว่า App ของคุณจะต้องมี Hardware Support BLE เท่านั้น */
<uses-feature android:name="android.hardware.bluetooth_le" android:required="true"/>
```

### Example
ตัวอย่างการ Scan BLE ด้วย Android
```java
  private BluetoothAdapter mBluetoothAdapter;
  private boolean mScanning;
  private Handler mHandler;

  private static final long SCAN_PERIOD = 10000;
  ...
  // ตรวจสอบอุปกรณ์ Support BLE
  if (!getPackageManager().hasSystemFeature(PackageManager.FEATURE_BLUETOOTH_LE)) {
    Toast.makeText(this, R.string.ble_not_supported, Toast.LENGTH_SHORT).show();
    finish();
  }
  
  // Initializes Bluetooth adapter.
  final BluetoothManager bluetoothManager =
          (BluetoothManager) getSystemService(Context.BLUETOOTH_SERVICE);
  mBluetoothAdapter = bluetoothManager.getAdapter();
  
  // ตรวจสอบการเปิดใช้งาน Bluetooth
  if (mBluetoothAdapter == null || !mBluetoothAdapter.isEnabled()) {
    Intent enableBtIntent = new Intent(BluetoothAdapter.ACTION_REQUEST_ENABLE);
    startActivityForResult(enableBtIntent, REQUEST_ENABLE_BT);
  }
  
  // คำสั่งในการค้นหาอุปกรณ์ BLE
  mBluetoothAdapter.startLeScan(mLeScanCallback);
  // คำสั่งในการหยุดการค้นหาอุปกรณ์
  mBluetoothAdapter.stopLeScan(mLeScanCallback);
  
  // Device scan callback.
  private BluetoothAdapter.LeScanCallback mLeScanCallback =
        new BluetoothAdapter.LeScanCallback() {
    @Override
    public void onLeScan(final BluetoothDevice device, int rssi,
            byte[] scanRecord) {
        
   }
};    
  

```
