## GateWay Payment Service With **Laravel** Framework

- Tap 
- My Fatoorah
- Stripe 
- Moyser 

### Integration With **Tap GateWay Payment**  

## How its work with this gateway ? 

### Step 1 :
> Create Services Folder **app/Services** after the add Class Service in Folder Sush as **TapService.php**
### step 2 : 
> IN the class TapService Create config with method payment 

```

(<?php

namespace App\Services;

use GuzzleHttp\Client;
use GuzzleHttp\Psr7\Request;

class TapPayment
{


    private $base_url;
    private $headers;
    private $request_client;

    public function __construct(Client $request_client)
    {
        $this->request_client = $request_client;
        $this->base_url = env('tap_base_url');
        $this->headers = [
            'Content-Type' => 'application/json',
            'authorization' => 'Bearer ' . 'sk_test_XKokBfNWv6FIYuTMg5sLPjhJ'
        ];
    }

    public function buildRequest($url, $method, $data = [])
    {
        $request = new Request($method, $this->base_url . $url, $this->headers);
        if (!$data)
            return false;
        $response = $this->request_client->send($request, [
            'json' => $data
        ]);
        if ($response->getStatusCode() != 200) {
            return false;
        }
        $response = json_decode($response->getBody(), true);
        return $response;
    }

    public function sendPayment($data)
    {
        return $response = $this->buildRequest('v2/charges', 'POST', $data);
    }

    public function getPaymentStatus($data)
    {
        return $response = $this->buildRequest('v2/getPaymentStatus', 'POST', $data);
    }
    public function getPaymentById($id)
    {
        return $response = $this->buildRequest('v2/charges/{id}', 'GET', $id);
    }


}
)
```
