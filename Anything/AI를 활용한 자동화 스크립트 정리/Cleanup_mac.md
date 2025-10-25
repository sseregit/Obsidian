```bash
#!/bin/bash

################################################################################
# macOS System Cleanup Script
# 자동 생성된 맥북 청소 스크립트
#
# 사용법:
#   ./cleanup_mac.sh              # 대화형 모드
#   ./cleanup_mac.sh --dry-run    # 테스트 모드 (실제 삭제 안함)
#   ./cleanup_mac.sh --all        # 모든 항목 자동 삭제 (위험!)
#   ./cleanup_mac.sh --help       # 도움말
################################################################################

# 색상 정의
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
BLUE='\033[0;34m'
NC='\033[0m' # No Color

# 플래그
DRY_RUN=false
AUTO_ALL=false
TOTAL_FREED=0

# 함수: 사용법 출력
show_help() {
    echo "macOS 시스템 청소 스크립트"
    echo ""
    echo "사용법:"
    echo "  $0                 대화형 모드 (각 단계별로 확인)"
    echo "  $0 --dry-run       테스트 모드 (실제 삭제하지 않음)"
    echo "  $0 --all           모든 항목 자동 삭제 (주의!)"
    echo "  $0 --help          이 도움말 표시"
    echo ""
    echo "예상 확보 가능 용량: ~131GB"
    echo ""
    exit 0
}

# 함수: 배너 출력
print_banner() {
    echo -e "${BLUE}╔══════════════════════════════════════════════════════════════╗${NC}"
    echo -e "${BLUE}║          macOS 시스템 청소 스크립트 v1.0                    ║${NC}"
    echo -e "${BLUE}║          총 예상 확보 용량: ~131GB                           ║${NC}"
    echo -e "${BLUE}╚══════════════════════════════════════════════════════════════╝${NC}"
    echo ""
}

# 함수: 크기 계산
get_size() {
    local path="$1"
    if [ -e "$path" ]; then
        du -sh "$path" 2>/dev/null | awk '{print $1}'
    else
        echo "0B"
    fi
}

# 함수: 사용자 확인
confirm() {
    local prompt="$1"
    local default="${2:-n}"

    if [ "$AUTO_ALL" = true ]; then
        return 0
    fi

    if [ "$default" = "y" ]; then
        read -p "$prompt [Y/n] " -n 1 -r
    else
        read -p "$prompt [y/N] " -n 1 -r
    fi
    echo
    [[ $REPLY =~ ^[Yy]$ ]]
}

# 함수: 안전한 삭제
safe_remove() {
    local path="$1"
    local description="$2"

    if [ ! -e "$path" ]; then
        echo -e "${YELLOW}  ⊘ 건너뜀: $description (존재하지 않음)${NC}"
        return 1
    fi

    local size=$(get_size "$path")

    if [ "$DRY_RUN" = true ]; then
        echo -e "${BLUE}  [DRY-RUN] 삭제 예정: $description ($size)${NC}"
        return 0
    fi

    echo -e "${GREEN}  ✓ 삭제 중: $description ($size)${NC}"
    rm -rf "$path"

    if [ $? -eq 0 ]; then
        echo -e "${GREEN}    성공!${NC}"
        return 0
    else
        echo -e "${RED}    실패!${NC}"
        return 1
    fi
}

# 함수: 명령어 실행
safe_execute() {
    local cmd="$1"
    local description="$2"

    if [ "$DRY_RUN" = true ]; then
        echo -e "${BLUE}  [DRY-RUN] 실행 예정: $description${NC}"
        echo -e "${BLUE}    명령어: $cmd${NC}"
        return 0
    fi

    echo -e "${GREEN}  ✓ 실행 중: $description${NC}"
    eval "$cmd"

    if [ $? -eq 0 ]; then
        echo -e "${GREEN}    성공!${NC}"
        return 0
    else
        echo -e "${RED}    실패!${NC}"
        return 1
    fi
}

################################################################################
# 청소 단계별 함수
################################################################################

# 1단계: Docker 정리 (최대 89GB)
cleanup_docker() {
    echo -e "\n${YELLOW}━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━${NC}"
    echo -e "${YELLOW}1단계: Docker 정리 (예상: ~89GB)${NC}"
    echo -e "${YELLOW}━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━${NC}"

    if ! command -v docker &> /dev/null; then
        echo -e "${YELLOW}  Docker가 설치되어 있지 않습니다. 건너뜁니다.${NC}"
        return
    fi

    echo "Docker 현재 상태:"
    docker system df
    echo ""

    if confirm "Docker를 정리하시겠습니까? (중지된 컨테이너, 빌드 캐시, 미사용 볼륨)"; then
        # 중지된 컨테이너 삭제
        safe_execute "docker container prune -f" "중지된 컨테이너 삭제"

        # 빌드 캐시 삭제
        if command -v docker-buildx &> /dev/null || docker buildx version &> /dev/null; then
            safe_execute "docker buildx prune --all -f" "빌드 캐시 삭제"
        fi

        # 미사용 볼륨 삭제
        if confirm "  미사용 Docker 볼륨도 삭제하시겠습니까? (데이터 손실 가능)"; then
            safe_execute "docker volume prune -f" "미사용 볼륨 삭제"
        fi

        # 전체 시스템 정리 (옵션)
        if confirm "  사용하지 않는 이미지도 모두 삭제하시겠습니까?"; then
            safe_execute "docker system prune -a -f" "전체 시스템 정리"
        fi

        echo ""
        echo "정리 후 Docker 상태:"
        docker system df
    fi
}

# 2단계: JetBrains 구버전 정리 (최대 10.5GB)
cleanup_jetbrains() {
    echo -e "\n${YELLOW}━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━${NC}"
    echo -e "${YELLOW}2단계: JetBrains 구버전 정리 (예상: ~10.5GB)${NC}"
    echo -e "${YELLOW}━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━${NC}"

    echo "현재 설치된 JetBrains 버전:"
    ls -d ~/Library/Caches/JetBrains/IntelliJIdea* 2>/dev/null | while read dir; do
        local size=$(get_size "$dir")
        echo "  - $(basename "$dir"): $size"
    done
    echo ""

    if confirm "JetBrains 구버전 캐시를 삭제하시겠습니까? (2025.2는 유지)"; then
        # 구버전 캐시 삭제
        safe_remove ~/Library/Caches/JetBrains/IntelliJIdea2024.3 "IntelliJ 2024.3 캐시"
        safe_remove ~/Library/Caches/JetBrains/IntelliJIdea2025.1 "IntelliJ 2025.1 캐시"
        safe_remove ~/Library/Caches/JetBrains/IntelliJIdea2024.2 "IntelliJ 2024.2 캐시"
        safe_remove ~/Library/Caches/JetBrains/IntelliJIdea2024.1 "IntelliJ 2024.1 캐시"
        safe_remove ~/Library/Caches/JetBrains/IntelliJIdea2023.1 "IntelliJ 2023.1 캐시"

        # 구버전 Application Support 삭제
        safe_remove ~/Library/Application\ Support/JetBrains/IntelliJIdea2024.3 "IntelliJ 2024.3 지원 파일"
        safe_remove ~/Library/Application\ Support/JetBrains/IntelliJIdea2025.1 "IntelliJ 2025.1 지원 파일"
        safe_remove ~/Library/Application\ Support/JetBrains/IntelliJIdea2024.2 "IntelliJ 2024.2 지원 파일"
        safe_remove ~/Library/Application\ Support/JetBrains/IntelliJIdea2024.1 "IntelliJ 2024.1 지원 파일"
        safe_remove ~/Library/Application\ Support/JetBrains/IntelliJIdea2023.1 "IntelliJ 2023.1 지원 파일"

        # 구버전 로그 삭제
        safe_remove ~/Library/Logs/JetBrains/IntelliJIdea2024.3 "IntelliJ 2024.3 로그"
        safe_remove ~/Library/Logs/JetBrains/IntelliJIdea2025.1 "IntelliJ 2025.1 로그"
        safe_remove ~/Library/Logs/JetBrains/IntelliJIdea2024.2 "IntelliJ 2024.2 로그"
        safe_remove ~/Library/Logs/JetBrains/IntelliJIdea2024.1 "IntelliJ 2024.1 로그"
        safe_remove ~/Library/Logs/JetBrains/IntelliJIdea2023.1 "IntelliJ 2023.1 로그"
    fi
}

# 3단계: 개발 도구 캐시 정리 (최대 18.5GB)
cleanup_dev_caches() {
    echo -e "\n${YELLOW}━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━${NC}"
    echo -e "${YELLOW}3단계: 개발 도구 캐시 정리 (예상: ~18.5GB)${NC}"
    echo -e "${YELLOW}━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━${NC}"

    # pip 캐시
    if command -v pip3 &> /dev/null; then
        local pip_size=$(get_size ~/Library/Caches/pip)
        echo "pip 캐시: $pip_size"
        if confirm "  pip 캐시를 삭제하시겠습니까?"; then
            safe_execute "pip3 cache purge" "pip 캐시 삭제"
        fi
    fi

    # npm 캐시
    if command -v npm &> /dev/null; then
        local npm_size=$(get_size ~/.npm)
        echo "npm 캐시: $npm_size"
        if confirm "  npm 캐시를 정리하시겠습니까?"; then
            safe_execute "npm cache verify" "npm 캐시 검증"
            safe_execute "npm cache clean --force" "npm 캐시 정리"
        fi
    fi

    # Homebrew 캐시
    if command -v brew &> /dev/null; then
        local brew_size=$(get_size ~/Library/Caches/Homebrew)
        echo "Homebrew 캐시: $brew_size"
        if confirm "  Homebrew 캐시를 정리하시겠습니까?"; then
            safe_execute "brew cleanup --prune=all -s" "Homebrew 캐시 정리"
            safe_execute "brew autoremove" "Homebrew 미사용 패키지 제거"
        fi
    fi

    # UV 캐시
    if command -v uv &> /dev/null; then
        local uv_size=$(get_size ~/.cache/uv)
        echo "UV 캐시: $uv_size"
        if confirm "  UV 캐시를 정리하시겠습니까?"; then
            safe_execute "uv cache clean" "UV 캐시 정리"
        fi
    fi

    # Gradle 캐시
    local gradle_size=$(get_size ~/.gradle/caches)
    if [ "$gradle_size" != "0B" ]; then
        echo "Gradle 캐시: $gradle_size"
        if confirm "  Gradle 빌드 캐시를 정리하시겠습니까?"; then
            safe_remove ~/.gradle/caches/build-cache-* "Gradle 빌드 캐시"
        fi
    fi

    # Anaconda 캐시
    if command -v conda &> /dev/null; then
        echo "Anaconda 패키지 캐시"
        if confirm "  Anaconda 캐시를 정리하시겠습니까?"; then
            safe_execute "conda clean --all -y" "Anaconda 캐시 정리"
        fi
    fi

    # node-gyp 캐시
    local nodegyp_size=$(get_size ~/Library/Caches/node-gyp)
    if [ "$nodegyp_size" != "0B" ]; then
        echo "node-gyp 캐시: $nodegyp_size"
        if confirm "  node-gyp 캐시를 삭제하시겠습니까?"; then
            safe_remove ~/Library/Caches/node-gyp "node-gyp 캐시"
        fi
    fi
}

# 4단계: 브라우저 캐시 정리 (최대 3.9GB)
cleanup_browser_caches() {
    echo -e "\n${YELLOW}━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━${NC}"
    echo -e "${YELLOW}4단계: 브라우저 캐시 정리 (예상: ~3.9GB)${NC}"
    echo -e "${YELLOW}━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━${NC}"

    local naver_size=$(get_size ~/Library/Caches/Naver)
    local brave_size=$(get_size ~/Library/Caches/BraveSoftware)
    local chrome_size=$(get_size ~/Library/Caches/Google/Chrome)

    echo "Naver Whale 캐시: $naver_size"
    echo "Brave 캐시: $brave_size"
    echo "Chrome 캐시: $chrome_size"
    echo ""

    if confirm "브라우저 캐시를 삭제하시겠습니까? (재로그인 필요할 수 있음)"; then
        safe_remove ~/Library/Caches/Naver "Naver Whale 캐시"
        safe_remove ~/Library/Caches/BraveSoftware "Brave 캐시"
        safe_remove ~/Library/Caches/Google/Chrome "Chrome 캐시"
    fi
}

# 5단계: 설치 파일 정리 (최대 3.7GB)
cleanup_installers() {
    echo -e "\n${YELLOW}━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━${NC}"
    echo -e "${YELLOW}5단계: Downloads 설치 파일 정리 (예상: ~3.7GB)${NC}"
    echo -e "${YELLOW}━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━${NC}"

    echo "Downloads 폴더의 DMG/설치 파일:"
    ls -lh ~/Downloads/*.dmg 2>/dev/null | awk '{print "  " $9 " (" $5 ")"}'
    echo ""

    if confirm "Downloads 폴더의 .dmg 설치 파일을 삭제하시겠습니까?"; then
        safe_remove ~/Downloads/ideaIU-2025.2.1-aarch64.dmg "IntelliJ 2025.2.1 설치 파일"
        safe_remove ~/Downloads/ideaIU-2024.2-aarch64.dmg "IntelliJ 2024.2 설치 파일"
        safe_remove ~/Downloads/Brave-Browser.dmg "Brave 설치 파일"
        safe_remove ~/Downloads/Claude.dmg "Claude 설치 파일"
        safe_remove ~/Downloads/Obsidian-1.8.7.dmg "Obsidian 설치 파일"
        safe_remove ~/Downloads/ChatGPT_Desktop_public_latest.dmg "ChatGPT 설치 파일"
    fi
}

# 6단계: 오래된 파일 정리 (최대 4.3GB)
cleanup_old_downloads() {
    echo -e "\n${YELLOW}━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━${NC}"
    echo -e "${YELLOW}6단계: Downloads 오래된 파일 정리 (예상: ~4.3GB)${NC}"
    echo -e "${YELLOW}━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━${NC}"

    echo "30일 이상 된 파일:"
    find ~/Downloads -type f -mtime +30 2>/dev/null | head -20
    local count=$(find ~/Downloads -type f -mtime +30 2>/dev/null | wc -l)
    echo "... (총 $count 개 파일)"
    echo ""

    echo -e "${RED}경고: 이 작업은 실수로 중요한 파일을 삭제할 수 있습니다.${NC}"
    if confirm "30일 이상 된 Downloads 파일을 삭제하시겠습니까?"; then
        if [ "$DRY_RUN" = true ]; then
            echo -e "${BLUE}[DRY-RUN] 삭제 예정 파일:${NC}"
            find ~/Downloads -type f -mtime +30 2>/dev/null
        else
            safe_execute "find ~/Downloads -type f -mtime +30 -delete" "30일 이상 된 파일 삭제"
        fi
    fi
}

# 7단계: 기타 대용량 파일 정리
cleanup_misc() {
    echo -e "\n${YELLOW}━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━${NC}"
    echo -e "${YELLOW}7단계: 기타 대용량 파일 정리 (예상: ~2.6GB)${NC}"
    echo -e "${YELLOW}━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━${NC}"

    # Java 힙 덤프
    local heapdump_size=$(get_size ~/java_error_in_idea.hprof)
    if [ "$heapdump_size" != "0B" ]; then
        echo "Java 힙 덤프 (크래시 파일): $heapdump_size"
        if confirm "  Java 힙 덤프를 삭제하시겠습니까?"; then
            safe_remove ~/java_error_in_idea.hprof "Java 힙 덤프"
        fi
    fi

    # HuggingFace 캐시
    local hf_size=$(get_size ~/.cache/huggingface)
    if [ "$hf_size" != "0B" ]; then
        echo "HuggingFace 모델 캐시: $hf_size"
        if confirm "  HuggingFace 모델 캐시를 삭제하시겠습니까? (ML 모델 재다운로드)"; then
            safe_remove ~/.cache/huggingface "HuggingFace 캐시"
        fi
    fi

    # Ollama 모델
    local ollama_size=$(get_size ~/.ollama)
    if [ "$ollama_size" != "0B" ]; then
        echo "Ollama AI 모델: $ollama_size"
        if confirm "  Ollama AI 모델을 삭제하시겠습니까? (AI 모델 재다운로드)"; then
            safe_remove ~/.ollama "Ollama 모델"
        fi
    fi
}

# 8단계: 최종 정리
final_cleanup() {
    echo -e "\n${YELLOW}━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━${NC}"
    echo -e "${YELLOW}8단계: 최종 시스템 정리${NC}"
    echo -e "${YELLOW}━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━${NC}"

    if confirm "휴지통을 비우시겠습니까?"; then
        safe_execute "rm -rf ~/.Trash/*" "휴지통 비우기"
    fi
}

################################################################################
# 메인 실행
################################################################################

main() {
    # 인자 파싱
    while [[ $# -gt 0 ]]; do
        case $1 in
            --dry-run)
                DRY_RUN=true
                shift
                ;;
            --all)
                AUTO_ALL=true
                shift
                ;;
            --help)
                show_help
                ;;
            *)
                echo "알 수 없는 옵션: $1"
                show_help
                ;;
        esac
    done

    # 배너 출력
    print_banner

    if [ "$DRY_RUN" = true ]; then
        echo -e "${BLUE}═══ DRY-RUN 모드 (실제로 삭제하지 않음) ═══${NC}\n"
    fi

    if [ "$AUTO_ALL" = true ]; then
        echo -e "${RED}═══ 자동 모드 (모든 항목 자동 삭제) ═══${NC}\n"
        echo -e "${RED}5초 후 시작합니다... (Ctrl+C로 취소)${NC}"
        sleep 5
    fi

    # 시작 시간 및 디스크 상태
    echo -e "${BLUE}청소 시작 전 디스크 상태:${NC}"
    df -h / | grep -E "Filesystem|/dev/"
    echo ""

    # 각 단계 실행
    cleanup_docker
    cleanup_jetbrains
    cleanup_dev_caches
    cleanup_browser_caches
    cleanup_installers
    cleanup_old_downloads
    cleanup_misc
    final_cleanup

    # 최종 결과
    echo -e "\n${GREEN}╔══════════════════════════════════════════════════════════════╗${NC}"
    echo -e "${GREEN}║                    청소 완료!                                ║${NC}"
    echo -e "${GREEN}╚══════════════════════════════════════════════════════════════╝${NC}\n"

    echo -e "${BLUE}청소 후 디스크 상태:${NC}"
    df -h / | grep -E "Filesystem|/dev/"
    echo ""

    if [ "$DRY_RUN" = true ]; then
        echo -e "${YELLOW}DRY-RUN 모드였습니다. 실제로 삭제하려면 --dry-run 없이 실행하세요.${NC}"
    fi
}

# 스크립트 실행
main "$@"

```