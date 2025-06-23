# morganavision-web
WebApp oficial de MorganaVision con integración PayPal
import { useEffect } from 'react';

export default function PayPalButton() {
  useEffect(() => {
    const script = document.createElement('script');
    script.src = "https://www.paypal.com/sdk/js?client-id=AQYGn6zTueVFPLKGX642LUq9k2S9ECqabOzP4NYlciLVcSnPYD0IkZ17cfQEhYiOux4y-PgdfqbQtcS5&vault=true&intent=subscription";
    script.setAttribute("data-sdk-integration-source", "button-factory");
    script.onload = () => {
      if (window.paypal) {
        window.paypal.Buttons({
          style: {
            shape: 'rect',
            color: 'gold',
            layout: 'vertical',
            label: 'paypal'
          },
          createSubscription: function (data, actions) {
            return actions.subscription.create({
              plan_id: 'P-55069314GE166910BNBM4UXQ'
            });
          },
          onApprove: function (data, actions) {
            alert("¡Gracias por suscribirte! ID: " + data.subscriptionID);
          }
        }).render('#paypal-button-container');
      }
    };
    document.body.appendChild(script);
  }, []);

  return <div id="paypal-button-container" />;
}
