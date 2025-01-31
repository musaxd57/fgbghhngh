import { useState, useEffect, useRef } from "react";

export default function PhoneVerification() {
  const [phone, setPhone] = useState("");
  const [otp, setOtp] = useState("");
  const [isOtpSent, setIsOtpSent] = useState(false);
  const [countdown, setCountdown] = useState(30);
  const phoneInputRef = useRef(null);

  useEffect(() => {
    if (phoneInputRef.current) {
      phoneInputRef.current.focus();
    }
  }, []);

  useEffect(() => {
    let timer;
    if (isOtpSent && countdown > 0) {
      timer = setInterval(() => {
        setCountdown((prev) => prev - 1);
      }, 1000);
    }
    return () => clearInterval(timer);
  }, [isOtpSent, countdown]);

  const sendOtp = () => {
    if (phone.length === 10) {
      setIsOtpSent(true);
      setCountdown(30);
      alert("Doğrulama kodu gönderildi!");
    } else {
      alert("Geçerli bir telefon numarası girin!");
    }
  };

  const verifyOtp = () => {
    if (otp.length === 6) {
      alert("Telefon doğrulandı!");
    } else {
      alert("Geçerli bir doğrulama kodu girin!");
    }
  };

  return (
    <div className="flex flex-col items-center p-6 space-y-4 bg-gray-100 min-h-screen">
      <h1 className="text-xl font-bold text-blue-600">Telefon Doğrulama</h1>
      {!isOtpSent ? (
        <>
          <label htmlFor="phone" className="font-medium">
            Telefon Numarası
          </label>
          <input
            id="phone"
            type="tel"
            ref={phoneInputRef}
            placeholder="Telefon Numarası (5551234567)"
            value={phone}
            onChange={(e) => setPhone(e.target.value)}
            className="border p-2 rounded"
          />
          <button onClick={sendOtp} className="bg-blue-600 text-white px-4 py-2 rounded">
            Kodu Gönder
          </button>
        </>
      ) : (
        <>
          <label htmlFor="otp" className="font-medium">
            Doğrulama Kodu
          </label>
          <input
            id="otp"
            type="number"
            placeholder="Doğrulama Kodu"
            value={otp}
            onChange={(e) => setOtp(e.target.value)}
            className="border p-2 rounded"
          />
          <p className="text-gray-600">Yeniden kod gönder: {countdown}s</p>
          <button onClick={verifyOtp} className="bg-blue-600 text-white px-4 py-2 rounded">
            Doğrula
          </button>
        </>
      )}
    </div>
  );
}
