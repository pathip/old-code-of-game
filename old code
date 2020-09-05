public class PlayerController : MonoBehaviour
{
    private int damage;
    private float speed = 1f;
    private float horizontalMove = 0f;
    private float jumpforce = 9f;
    private float jumppower = 10f;
    private int jumpCount = 2;
    private float NonWeaponAttackRate = 0.2f;
    private float NextNonWeaponAttack = 0.0f;
    private float WeaponAttackRate = 0.2f;
    private float NextWeaponAttack = 0.0f;
    const float GroundedRadius = .2f;
    private bool grounded;
    const float CeilingRadius = .2f;
    private bool jump;
    private bool doublejump;
    private bool jumpattack;
    private bool getweapon = false;
    public Transform GroundCheck;
    private Animator animator;
    private Weapon weaponepuipped;
    private AttackwithWeapon attackwithWeapon;
    private Rigidbody2D Rigidbody2D;
    private bool FacingRight = true;
    private Vector3 Velocity = Vector3.zero;
    private Physics2D Physics2D;
    public int heath = 100;
    public int maxheath = 100;
    public int mana = 50;
    public int maxmana = 50;
    public int soul = 0;
    public Text UIheath,UIsoul;
    public Slider slidermana;
    void Start()
    {
        Rigidbody2D = this.gameObject.GetComponent<Rigidbody2D>();
        //animator = this.gameObject.GetComponent<Animator>();
        attackwithWeapon = this.gameObject.GetComponentInChildren<AttackwithWeapon>();
        slidermana.maxValue = maxmana;
        slidermana.value = mana;
    }

    void Update()
    {
        grounded = true;
        if(Input.GetAxis("Horizontal") < -0.1f)
        {
            transform.Translate(Vector2.right * speed * Time.deltaTime);
            transform.eulerAngles = new Vector2(0, 180);
        }
        else if (Input.GetAxis("Horizontal") > 0.1f)
        {
            transform.Translate(Vector2.right * speed * Time.deltaTime);
            transform.eulerAngles = new Vector2(0, 0);
        }
        UIheath.text = heath + " / " + maxheath;
        UIsoul.text = "Souls : " + soul;
        slidermana.value = mana;
        if (heath <= 0)
        {
            heath = 0;
            animator.SetTrigger("Death");
        }

        if (grounded || !doublejump)
        {
            grounded = false;
            jumpCount++;
            jump = true;
            Rigidbody2D.AddForce(jumpforce * (Vector2.up * jumppower));
            if (!doublejump && !grounded)
            {
                jumpCount++;
                doublejump = true;
                Rigidbody2D.AddForce(jumpforce * (Vector2.up * jumppower));
            }
        }

        if (!getweapon)
        {
            NextNonWeaponAttack = Time.time + NonWeaponAttackRate;
            damage = 10;
        }
        else if (getweapon)
        {
            NextWeaponAttack = Time.time + WeaponAttackRate;
            attackwithWeapon.playanimation(weaponepuipped.animation);
        }
    }

    public void AddWeapon(Weapon weapon)
    {
        weaponepuipped = weapon;
        getweapon = true;
        attackwithWeapon.SetWeapon(weaponepuipped.Damage);
    }

    private void OnTriggerEnter2D(Collider2D other)
    {
        if(other.gameObject.tag == "Soul")
        {
            soul = soul + 10;
            Destroy(other.gameObject);
        }
    }
}
