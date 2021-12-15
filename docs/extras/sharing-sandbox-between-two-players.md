The current philosophy of KYPO CRP follows the idea that each trainee works in his or her isolated sandbox. However, sometimes it is useful to share a sandbox, e.g., to enable attack-defense games where both attacker and defended share a network. KYPO doesn't support this sharing natively (via web GUI), but this functionality can be achieved with some effort and restrictions. Moreover, the described process can be easily extended to enable access for more than two players.

## Preparation

* **Sandbox definition:** If the secondary trainee (typically an attacker) should remain unnoticed by the primary trainee, then it is necessary to define one or more hidden hosts (`hidden: True` in the `topology.yml` definition) that serve as access points for the second player.
* **Training instance:** Make a note of the sandbox id for later use.

## Access during the training session
* The **primary trainee** can use the KYPO web portal to access hosts comfortably, as usual. 
* The **secondary trainee** gets access as follows:

    1. Connect and authenticate to the KYPO Portal.
    2. Copy the Bearer token from the browser. In Google Chrome, open the `Developer Console` (F12), go to the local storage (`Application -> Local Storage -> KYPO Portal URL -> access_token`)
    3. Use [Postman](https://www.postman.com/) application to generate an HTTP console request:

        1. Use endpoint `https://docs.crp.kypo.muni.cz/reference/kypo-sandbox-service-swagger-open-api/#/sandboxes/sandboxes_vms_console_list{KYPO}/sandboxes/{sandbox_id}/vms/{vm_name}/console`,
      where `{KYPO}` is current instance of KYPO CRP, `{sandbox_id}` is a unique identifier of the sandbox, and `{vm_name}` is the name of the hidden host.
        2. Use the `Bearer Token` authorization type in the `Authorization` section and provide the bearer token from the Developer console.
        3. You get JSON with a link to the console.

!!! info "Secondary trainees"
    More than one secondary trainee can access the sandbox in the same way.

!!! warning "Token expiration" 
    The token is valid for **only two hours**. Then a new token has to be generated.

