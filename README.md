# foodpanda-total
Check how much money you've spent in total on foodpanda.pk

Copy and paste the following script in your browser's console or any other js vm.

Navigate to foodpanda.pk.
Press F12, switch to the applications tab and replace the authorization header's JWT token with your JWT authorization token stored in Cookies -> 'token' for the foodpanda.pk domain.

```
fetch("https://pk.fd-api.com/api/v5/orders/order_history?include=order_products,order_details&limit=0", {
  "headers": {
    "accept": "application/json, text/plain, */*",
    "accept-language": "en-US,en;q=0.9",
    "authorization": "Bearer
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5ceyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
    "x-fp-api-key": "volo",
    "x-pd-language-id": "1"
  },
  "method": "GET",
  "mode": "cors",
  "credentials": "include"
}).then(res => res.json()).then(res => {
    let total = res.data.items.reduce((prev, curr) => {
        if (curr.decline_reason) return prev;
        return prev + curr.total_value
    }, 0);
    console.log(`Total money spent on foodpanda: ${total}`);
});
```
