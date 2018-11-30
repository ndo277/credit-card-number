#include <stdio.h>
#include <cs50.h>
#include <math.h>

int main(void)
{
    //declare cc variable as long long
    long long cc_num;

    //prompt for CC#
    do
    {
        cc_num = get_long_long("Number: ");
    }
    //must be positive
    while (cc_num < 0);

    //getting 2nd to last digit
    //first move cc_num decimal point one digit to the left
    //and assign to new variable as double (large float)
    //preserve original cc_num for digit brand-checking later
    double cc_num_new = cc_num / 10;

    //cast as long long to truncate decimals and be able to use % on it
    long long cc_num_long = cc_num_new;

    //use % 10 to get 2nd to last digit of cc_num (last digit of cc_num_long)
    int sec_digit = cc_num_long % 10;



    //declare and initialize first half total of CC digits
    int totalA;
    //if single-digit after digit*2
    if (sec_digit * 2 < 10)
    {
        //intial sum is just the product of digit*2
        totalA = sec_digit * 2;
    }
    //if double-digits after digit*2
    else
    {
        //intial sum = product's one's place digit PLUS its ten's place digit
        totalA = (sec_digit * 2 % 10) + (sec_digit * 2 / 10 % 10);
    }

    //adding total to sum of every other digit*2's digits
    //stop when cc_num has no digits left
    while (cc_num_long > 0)
    {

        //shortening cc_num_long and skipping every other digit
        cc_num_long = cc_num_long / 100;
        //get every other digit
        int next_digit = cc_num_long % 10;
        //if single-digit
        if (next_digit * 2 < 10)
        {
            //total is just product of digit*2
            totalA += next_digit * 2;

        }

        //if double-digit
        else
        {
            //total is the sum of each digit of next_digit*2
            totalA += (next_digit * 2 % 10) + (next_digit * 2 / 10 % 10);
        }
    }



    //2nd half of CC num digits
    //get last digit of cc_num
    int last_digit = cc_num % 10;


    //declare and initialize 2nd half sum of CC digits w/ last digit
    int totalB = last_digit;

    //skip to every other digit
    double cc_num_next = cc_num / 100;
    //truncate decimals
    long long cc_num_ll = cc_num_next;
    //get last digit
    int other_digit = cc_num_ll % 10;

    //stop when no more digits
    while (cc_num_ll > 0)
    {
        //add last digit to 2nd half total
        totalB += other_digit;
        //skip to every other digit
        cc_num_ll = cc_num_ll / 100;
        //get next digit
        other_digit = cc_num_ll % 10;

    }


    //checking MASTERCARD, AMEX, VISA, or INVALID

    //cc_num invalid if checksum is not a multiple of ten
    int checksum = totalA + totalB;
    if (checksum % 10 != 0)
    {
        printf("INVALID\n");
    }
    else if (checksum % 10 == 0)
    {
        //initialize rolling sum to count number of digits minus 2
        int count = 0;
        //check first two digits by dividing cc_num by 10 until < 100
        while (cc_num >= 100)
        {
            cc_num = cc_num / 10;
            count += 1;
        }
        //truncate by converting to int
        int cc_num_int = cc_num;

        //get first two digits and compare
        //AMEX = 34 or 37 and 15 digits long
        if (count == 13 && (cc_num_int == 34 || cc_num_int == 37))
        {
            printf("AMEX\n");
        }
        //MC = 51, 52, 53, 54, or 55 and 16 digits long
        else if (count == 14 && (cc_num_int >= 51 && cc_num_int <= 55))
        {
            printf("MASTERCARD\n");
        }
        //if not MC/AmEx, check if Visa by converting to one digit
        else
        {
            //get first digit
            int cc_num_first = cc_num_int / 10;
            //VISA = 4... and 13 or 16 digits long
            if ((count == 11 || count == 14) && cc_num_first == 4)
            {
                printf("VISA\n");
            }
            else
            {
                printf("INVALID\n");
            }
        }
    }
}
