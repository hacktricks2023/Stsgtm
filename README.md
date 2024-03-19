pkg update 

pkg upgrade 

pkg install dnsutils -y


#!/bin/bash

clear

function endscript() {
  exit 1
}

trap endscript 2 15

echo -e "\e[1;37mEnter DNS IPs separated by ' ': \e[0m"
read -a DNS_IPS

echo -e "\e[1;37mEnter Your NameServers separated by ' ': \e[0m"
read -a NAME_SERVERS

LOOP_DELAY=3
echo -e "\e[1;37mCurrent loop delay is \e[1;33m${LOOP_DELAY}\e[1;37m seconds.\e[0m"
  
  fi
fi

DIG_EXEC="DEFAULT"
CUSTOM_DIG=/data/data/com.termux/files/home/go/bin/fastdig
VER=0.3

case "${DIG_EXEC}" in
  DEFAULT|D)
    _DIG="$(command -v dig)"
    ;;
  CUSTOM|C)
    _DIG="${CUSTOM_DIG}"
    ;;
esac

if [ ! $(command -v ${_DIG}) ]; then
  printf "%b" "Dig command failed to run, please install dig(dnsutils) or check the DIG_EXEC & CUSTOM_DIG variable.\n" && exit 1
fi

# Initialize the counter
count=1

check(){
  local border_color="\e[96m"  # Light blue color
  local success_color="\e[92m"  # Light green color
  local fail_color="\e[91m"    # Light red color
  local header_color="\e[96m"  # Light blue color
  local reset_color="\e[96m"    # Reset to default terminal color
  local padding="  "            # Padding for aesthetic

  # Header
  echo -e "${border_color}%====ðŸŒŒ=====UpTime====DNS=IP=GTM===========ðŸŒŒ====%${reset_color}"
  echo -e "${border_color}│${header_color}${padding}DNS Status Check Results${padding}${reset_color}"
  echo -e "${border_color}├──────────────────────────────────────────────┤${reset_color}"
  
  # Results
  for T in "${DNS_IPS[@]}"; do
    for R in "${NAME_SERVERS[@]}"; do
      result=$(${_DIG} @${T} ${R} +short)
      if [ -z "$result" ]; then
        STATUS="${success_color}Success${reset_color}"
      else
        STATUS="${fail_color}Failed${reset_color}"
      fi
      echo -e "${border_color}│${padding}${reset_color}DNS IP: ${T}${padding}${reset_color}"
      echo -e "${border_color}│${padding}NameServer: ${R}${padding}${reset_color}"
      echo -e "${border_color}│${padding}Status: ${STATUS}${padding}${reset_color}"
    done
  done

  # Check count and Loop Delay
  echo -e "${success_color}%========================JMT=TEAM====================%${reset_color}"
  echo -e "${border_color}│${padding}${header_color}Check count: ${count}${padding}${reset_color}"
  echo -e "${border_color}│${padding}Loop Delay: ${LOOP_DELAY} seconds${padding}${reset_color}"
 
  # Footer
  echo -e "${success_color}%========================VanTricks===================%%%%%%%%%%%%%%%%%%=End=Auto Refresh=%%%%%%%%%%%%%%%%%%%${reset_color}"
}

countdown() {
    for i in 3 2 1 0; do
        echo "Checking started in $i seconds..."
        sleep 1
    done
}
echo""
echo""
echo "NEED LEGIT INTERNET...."
echo""
echo""
echo""
countdown
  clear

# Main loop
while true; do
  check
  ((count++))  # Increment the counter
  echo""
  echo""
  echo""
  echo""
  echo""
  echo""
  echo""
  
done

exit 0
