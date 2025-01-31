import { useState, useEffect } from "react";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";

export default function PhoneVerification() {
  const [phone, setPhone] = useState("");
  const [otp, setOtp] = useState("");
  const [isOtpSent, setIsOtpSent] = useState(false);
  const [countdown, setCountdown] = useState(30);

  useEffect(() => {
    let timer;
    if (isOtpSent && countdown > 0) {
      timer = setInterval(() => setCountdown((prev) => prev - 1), 1000);
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
      <h1 className="text-xl font-bold">Telefon Doğrulama</h1>
      {!isOtpSent ? (
        <>
          <label htmlFor="phone">Telefon Numarası</label>
          <Input
            id="phone"
            type="tel"
            placeholder="Telefon Numarası (5551234567)"
            value={phone}
            onChange={(e) => setPhone(e.target.value)}
          />
          <Button onClick={sendOtp}>Kodu Gönder</Button>
        </>
      ) : (
        <>
          <label htmlFor="otp">Doğrulama Kodu</label>
          <Input
            id="otp"
            type="number"
            placeholder="Doğrulama Kodu"
            value={otp}
            onChange={(e) => setOtp(e.target.value)}
          />
          <p className="text-gray-600">Yeniden kod gönder: {countdown}s</p>
          <Button onClick={verifyOtp}>Doğrula</Button>
        </>
      )}
    </div>
  );
}
