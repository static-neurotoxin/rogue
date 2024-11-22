cmake_minimum_required(VERSION 3.16)
project(Rogue VERSION 5.4.4 LANGUAGES C)

find_package(Curses REQUIRED)

# Options
option(WITH_PROGRAM_NAME "Alternate executable name" OFF)
option(ENABLE_SETGID "Install executable as setgid" OFF)
option(ENABLE_SCOREFILE "Enable scoreboard file" OFF)
option(ENABLE_LOCKFILE "Enable scoreboard lockfile" OFF)
option(ENABLE_WIZARDMODE "Enable wizard mode" OFF)
option(ENABLE_ALLSCORES "Enable allscores feature" ON)
option(ENABLE_CHECKTIME "Enable checktime" OFF)
option(ENABLE_MAXLOAD "Enable maxload" OFF)
option(ENABLE_MAXUSERS "Enable maxusers" OFF)

# Configure definitions and substitutions
set(PROGRAM_NAME "rogue")
if(WITH_PROGRAM_NAME)
  set(PROGRAM_NAME "${WITH_PROGRAM_NAME}")
endif()

if(ENABLE_SETGID)
  add_definitions(-DGROUPOWNER="games")
endif()

if(ENABLE_SCOREFILE)
  set(SCOREFILE "${PROGRAM_NAME}.scr")
  add_definitions(-DSCOREFILE="${SCOREFILE}")
endif()

if(ENABLE_LOCKFILE)
  set(LOCKFILE "${PROGRAM_NAME}.lck")
  add_definitions(-DLOCKFILE="${LOCKFILE}")
endif()

if(ENABLE_WIZARDMODE)
  add_definitions(-DMASTER)
endif()

if(ENABLE_ALLSCORES)
  add_definitions(-DALLSCORES=1)
endif()

if(ENABLE_CHECKTIME)
  add_definitions(-DCHECKTIME=1)
endif()

# Header file checks
include(CheckIncludeFile)
check_include_file("arpa/inet.h" HAVE_ARPA_INET_H)
check_include_file("sys/utsname.h" HAVE_SYS_UTSNAME_H)
# Add more checks as needed...

# Generate `config.h` based on the checks
configure_file(config.h.in config.h)

# Source files
set(SOURCES
        armor.c      
        daemon.c     
        fight.c      
        list.c       
        mdport.c     
        move.c       
        pack.c       
        rings.c      
        save.c       
        sticks.c     
        weapons.c
        chase.c      
        daemons.c    
        init.c       
        mach_dep.c   
        misc.c       
        new_level.c  
        passages.c   
        rip.c        
        scrolls.c    
        things.c     
        wizard.c
        command.c    
        extern.c     
        io.c         
        main.c       
        monsters.c   
        options.c    
        potions.c    
        rooms.c      
        state.c      
        vers.c       
        xcrypt.c
)

# Build target
add_executable(${PROGRAM_NAME} ${SOURCES})
target_include_directories(${PROGRAM_NAME} PRIVATE ${CMAKE_BINARY_DIR} ${CURSES_INCLUDE_DIR})
target_compile_definitions(${PROGRAM_NAME} PRIVATE $<$<BOOL:${ENABLE_WIZARDMODE}>:MASTER>)
target_link_libraries(${PROGRAM_NAME} PRIVATE ${CURSES_LIBRARIES})
# Install rules
install(TARGETS ${PROGRAM_NAME} RUNTIME DESTINATION bin)